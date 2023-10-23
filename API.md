---
description: La consommation d'une API avec Symfony
---

# Consommer une API

Les API sont le liant entre les applications. Elles permettent de récupérer des données d'une application à une autre. Elles sont donc très utiles pour les applications mobiles, les applications web, les applications de bureau, etc.

# Pourquoi consommer une API ?

- Pour avoir accès à des données dont vous ne disposez pas ou qu'il serait trop long et coûteux de développer vous-même.
- Pour utiliser des services externes à votre application (paiement en ligne, envoi de mail, envoi de SMS, etc.)

Vous voyez donc que les API sont très utiles et qu'il est important de savoir les consommer dans vos applications web.

## Comment consommer une API avec Symfony ?

Il existe plusieurs manières de consommer une API avec Symfony. Nous allons voir comment le faire avec Stripe, un service de paiement en ligne.

Contexte, vous avez un site web commerçant et vous souhaitez proposer le paiement en ligne à vos clients. Vous allez donc utiliser Stripe pour gérer les paiements. Nous allons voir ensemble comment mettre cela en place à partir de l'**étape du paiement**.

**Thème : Location de salle de réunion**
1. L'internaute visite le site web
2. Ajout des produits ou service dans un panier
3. Validation de la commande
4. Paiement de la commande <- À PARTIR D'ICI
5. Validation du paiement
6. Gestion de la commande

### Installer le SDK Stripe

Pour commencer, il faut installer le SDK Stripe dans votre projet Symfony. Pour cela, il faut utiliser Composer.

```bash
composer require stripe/stripe-php
```

### Créer un compte Stripe

Ensuite, il faut créer un compte Stripe. C'est sur ce compte que vous allez gérer vos paiements. Vous pouvez créer un compte sur [le site de Stripe](https://dashboard.stripe.com/register). Puis récupérez votre clé secrète et votre clé publique depuis votre tableau de bord "Développeurs" > "Clés API".

Une fois que vous avez récupéré vos clés, il faut les ajouter dans votre fichier `.env` :

```env
# .env ou .env.local

STRIPE_SECRET_KEY=sk_test_51J4XXXXXXXXXXXXXXXXXXXXXXX
STRIPE_PUBLIC_KEY=pk_test_51J4XXXXXXXXXXXXXXXXXXXXXXX
```

Ce n'est pas tout, il faut aussi ajouter la référence de ces clés dans votre fichier `services.yaml` :

```yaml
# config/services.yaml

parameters:
    # ...
    STRIPE_SECRET_KEY: '%env(STRIPE_SECRET_KEY)%'
    STRIPE_PUBLIC_KEY: '%env(STRIPE_PUBLIC_KEY)%'
``` 

Cette configuration permet de rendre vos clés accessibles dans votre application Symfony de manière globale. Il suffit de les appeler avec `$this->getParameter('STRIPE_SECRET_KEY')` et `$this->getParameter('STRIPE_PUBLIC_KEY')`.

### Créer un controller pour gérer le paiement

Maintenant, il faut créer un controller pour gérer le paiement. Pour cela, créez un controller `PaymentController` avec la commande suivante :

```bash
symfony console make:controller PaymentController
```

Maintenant nous pouvons mettre en place le nécessaire pour gérer le paiement. Pour rappel l'exemple ici est le paiement d'une location de salle de réunion. Nous allons donc créer une route qui va permettre de créer une session de paiement Stripe. Cette session va contenir les informations de la commande et permettre à l'internaute de payer. Retrouvez la documentation de Stripe sur [Checkout](https://stripe.com/docs/payments/checkout).

```php
# src/Controller/PaymentController.php

// ...

use Stripe\Stripe;
use Stripe\Checkout\Session;
use App\Repository\OrderRepository;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\RedirectResponse;

class PaymentController extends AbstractController
{
    #[Route('payment/session', name: 'payment_session')]
    public function paymentSession(Request $request, OrderRepository $orderRepository): RedirectResponse
    {
        // Configuration de Stripe avec la clé secrète
        Stripe::setApiKey($this->getParameter('STRIPE_SECRET_KEY'));

        /**
         * Récupérez les informations de la commande 
         * depuis la base de données ou via request
         * Faites comme vous le souhaitez,
         * elles doivent juste être accessibles ici
         */
        $order = $orderRepository->findOneBy([
            'id' => $request->get('order')
        ]);

        // Création de la session de paiement Stripe
        if($order){
            $checkout_session = Session::create([
                'payment_method_types' => ['card'],
                'line_items' => [[
                    'price_data' => [
                        'currency' => 'eur',
                        'unit_amount' => $order->getTotal() * 100, // Stripe utilise des centimes
                        'product_data' => [ // Les informations du produit sont personnalisables
                            'name' => 'Réservation',
                        ],
                    ],
                    'quantity' => 1,
                ]],
                'mode' => 'payment',
                'success_url' => $this->generateUrl('payment_success', ['order' => $order->getId()], 0),
                'cancel_url' => $this->generateUrl('payment_cancel', [], 0),
            ]);

            // Redirection vers la page de paiement
            return $this->redirect($checkout_session->url);
        }
    }
}
```

### Créer les routes Success et Cancel

Maintenant, il faut créer les routes `payment_success` et `payment_cancel` qui vont permettre de gérer l'affichage de la page pour le succès ou l'échec du paiement. 

```php
# src/Controller/PaymentController.php

// ...

    #[Route('payment/success', name: 'payment_success')]
    public function paymentSuccess(
        Request $request,
        OrderRepository $orderRepository
    ): Response
    {
        $order = $orderRepository->findOneBy([
            'id' => $request->get('order')
        ]);
        $order->setStatut(true);
        return $this->render('payment/success.html.twig', [
            'order' => $order
        ]);
    }

    #[Route('payment/cancel', name: 'payment_cancel')]
    public function paymentCancel(): Response
    {
        return $this->render('payment/cancel.html.twig');
    }
```

### Créer les templates

N'oubliez pas de créer les templates `payment/success.html.twig` et `payment/cancel.html.twig` pour afficher les pages de succès et d'échec du paiement. Vous pouvez les personnaliser comme vous le souhaitez.

---

Voici un exemple de code pour consommer une API avec Symfony. Vous pouvez bien évidemment l'adapter à vos besoins. Vous pouvez aussi utiliser d'autres services de paiement en ligne comme [PayPal](https://developer.paypal.com/docs/api/overview/) ou [MangoPay](https://docs.mangopay.com/).

Ce qu'il faut retenir, c'est que les API sont très utiles et qu'il est important de savoir les consommer dans vos applications web afin d'améliorer l'expérience utilisateur.