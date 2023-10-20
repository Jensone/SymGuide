---
description: Les formulaires dans Symfony
---

# Les formulaires

Symfony rend la création de formulaires facile avec l'aide de ses composants Form et Validator. Ils sont indépendants du moteur de rendu et peuvent être utilisés dans n'importe quelle application web. Les formulaires peuvent être créés, rendus et traités. Les données sont stockées dans des objets PHP qui peuvent être persistés dans une base de données ou envoyés par e-mail.

# Pourquoi faire des formulaires ?

Les formulaires sont un élément essentiel de tout site et applications web. Ils permettent aux utilisateurs de saisir des données, qui sont ensuite envoyées au serveur pour traitement. Les formulaires sont utilisés pour tout, des simples formulaires de contact aux formulaires d'inscription complexes avec des règles de validation et des champs imbriqués.

## Les formulaires dans Symfony

Pour créer un formulaire, il faut créer une classe PHP qui hérite de la classe `AbstractType` et implémente l'interface `FormBuilderInterface`. Cette classe contient les champs du formulaire et leurs options. Elle peut être utilisée pour générer le code HTML du formulaire et pour valider les données soumises par l'utilisateur.

Nous allons utiliser Symfony CLI pour créer un formulaire. Dans le terminal, à la racine du projet, exécuter la commande suivante :

```bash
# Création d'un formulaire
symfony console make:form
```

Il faut ensuite renseigner le nom de la classe du formulaire. Par exemple, pour un formulaire de contact, on peut renseigner `CandidateType`.

Le formulaire est créé dans le dossier `src/Form`. Il contient une classe `CandidateType` qui hérite de la classe `AbstractType` et implémente l'interface `FormBuilderInterface`.

```php
# src/Form/CandidateType.php
<?php

namespace App\Form;

use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;

class CandidateType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options)
    {
        $builder
            ->add('firstname')
            ->add('lastname')
            ->add('email')
            ->add('phone')
            ->add('cv')
            ->add('message')
            ->add('sendAt')
            ->add('job')
            ->add('submit')
        ;
    }

    public function configureOptions(OptionsResolver $resolver)
    {
        $resolver->setDefaults([
            // Configure your form options here
        ]);
    }
}
```

## Les champs du formulaire

Les champs du formulaire sont ajoutés à l'aide de la méthode `add()` de l'objet `$builder`. Cette méthode prend deux arguments : le nom du champ et le type de champ. Afin de configurer le champs avec la spécification du type, des assertions et options, vous devez charger les TypeExtensions appropriées :

```php
# src/Form/CandidateType.php

// ...

use Symfony\Component\Form\Extension\Core\Type\TextType;
use Symfony\Component\Form\Extension\Core\Type\EmailType;
use Symfony\Component\Form\Extension\Core\Type\TelType;
use Symfony\Component\Form\Extension\Core\Type\TextareaType;
use Symfony\Component\Form\Extension\Core\Type\DateTimeType;
use Symfony\Component\Form\Extension\Core\Type\ChoiceType;
use Symfony\Component\Form\Extension\Core\Type\SubmitType;

class CandidateType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options)
    {
        $builder
            ->add('firstname', TextType::class, [
                'label' => 'Prénom',
                'attr' => [
                    'placeholder' => 'Votre prénom',
                    'class' => 'form-control'
                ]
            ])
            ->add('lastname', TextType::class, [
                'label' => 'Nom',
                'attr' => [
                    'placeholder' => 'Votre nom',
                    'class' => 'form-control'
                ]
            ])
            ->add('email', EmailType::class, [
                'label' => 'Email',
                'attr' => [
                    'placeholder' => 'Votre email',
                    'class' => 'form-control'
                ]
            ])
            ->add('phone', TelType::class, [
                'label' => 'Téléphone',
                'attr' => [
                    'placeholder' => 'Votre téléphone',
                    'class' => 'form-control'
                ]
            ])
            ->add('cv')
            ->add('message', TextareaType::class)
            ->add('sendAt', DateTimeType::class)
            ->add('job', ChoiceType::class, [
                'choices' => [
                    'Développeur Symfony' => 'Développeur Symfony',
                    'Développeur Laravel' => 'Développeur Laravel',
                    'Développeur Drupal' => 'Développeur Drupal',
                    'Développeur React' => 'Développeur React',
                    'Développeur Wordpress' => 'Développeur Wordpress'
                ],
                'label' => 'Poste souhaité',
                'attr' => [
                    'class' => 'form-control'
                ]
            ])
            ->add('Postuler', SubmitType::class)
        ;
    }

    // ...
}
```

## Les options du formulaire

Comme vous pouvez le voir dans l'exemple précédent, la méthode `add()` prend un troisième argument qui est un tableau d'options. Ces options sont utilisées pour configurer le champ. Par exemple, l'option `label` permet de définir le label du champ. L'option `attr` permet de définir les attributs HTML du champ.

Vous avez peut-être remarque qu'aucun argument n'était passer pour `->add('cv')`. Voyons en détail comment configurer ce champ pour uploader un fichier de type PDF avec `FileType` :

1. Créer un dossier `uploads` à la racine du projet dans lequel seront stockés les fichiers uploadés.
2. Renseigner le chemin du dossier `uploads` dans le fichier `services.yaml` :

```yaml
# config/services.yaml
parameters:
    uploads_directory: '%kernel.project_dir%/uploads'
```
3. Ajouter l'option `mapped` à `false` pour indiquer que ce champ n'est pas lié à une propriété de l'entité (dans le cas d'un formulaire de création d'entité) :

```php
# src/Form/CandidateType.php

// ...

->add('cv', FileType::class, [
    'mapped' => false
])

// ...
```
4. Ajouter l'option `constraints` pour définir les contraintes de validation du champ :

```php
# src/Form/CandidateType.php

// ...
use Symfony\Component\Validator\Constraints\File;

// ...

->add('cv', FileType::class, [
    'mapped' => false,
    'constraints' => [
        new File([
            'maxSize' => '1024k',
            'mimeTypes' => [
                'application/pdf',
                'application/x-pdf',
            ],
            'mimeTypesMessage' => 'Veuillez uploader un fichier PDF valide',
        ])
    ]
])

// ...
```

## Afficher et traiter le formulaire

Pour afficher le formulaire, il faut l'injecter dans le contrôleur :

```php
# src/Controller/CandidateController.php

// ...

use App\Form\CandidateType;
use Symfony\Component\Mime\Email;
use Symfony\Component\Mailer\MailerInterface;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Annotation\Route;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;

class CandidateController extends AbstractController
{
    #[Route('/candidature', name: 'candidate', methods: ['GET', 'POST'])]
    public function new(Request $request): Response
    {
        $form = $this->createForm(CandidateType::class);
        $form->handleRequest($request);

        if ($form->isSubmitted() && $form->isValid()) {
            
            if ($form->get('cv')->getData()) {
                $cvFile = $form->get('cv')->getData();
                $originalFilename = pathinfo($cvFile->getClientOriginalName(), PATHINFO_FILENAME);
                $newFilename = $originalFilename.'-'.uniqid().'.'.$cvFile->guessExtension();

                try {
                    $cvFile->move(
                        $this->getParameter('uploads_directory'),
                        $newFilename
                    );
                } catch (FileException $e) {
                    $this->addFlash('danger', 'Une erreur est survenue lors de l\'upload de votre CV');
                }
            }

            $mail = (new Email())
                ->from($form->get('email')->getData())
                ->to('contact@symguide.com')
                ->subject('Nouvelle candidature de '.$form->get('firstname')->getData().' '.$form->get('lastname')->getData())
                ->priority(Email::PRIORITY_HIGH)
                ->text($form->get('message')->getData())
                ->html('<p>Nouvelle candidature<br>'.$form->get('message')->getData().'</p>')
                ->attachFromPath($this->getParameter('uploads_directory').'/'.$newFilename)
            ;

            $mailer->send($mail);

            $this->addFlash('success', 'Votre candidature a bien été envoyée !');

            return $this->redirectToRoute('candidate');
        }

        return $this->render('candidate/new.html.twig', [
            'form' => $form
        ]);
    }
}
```

Pour afficher le formulaire dans le template, il faut utiliser la méthode `createView()` de l'objet `$form` :

```
# templates/candidate/new.html.twig
{% extends 'base.html.twig' %}

{% block title %}Candidature{% endblock %}

{% block body %}
    <h1>Candidature</h1>

    {% for label, messages in app.flashes %}
        {% for message in messages %}
            <div class="alert alert-{{ label }}">
                {{ message }}
            </div>
        {% endfor %}
    {% endfor %}

    {{ form_start(form) }}
        {{ form_row(form.firstname) }}
        {{ form_row(form.lastname) }}
        {{ form_row(form.email) }}
        {{ form_row(form.phone) }}
        {{ form_row(form.cv) }}
        {{ form_row(form.message) }}
        {{ form_row(form.sendAt) }}
        {{ form_row(form.job) }}
        {{ form_row(form.submit) }}
    {{ form_end(form) }}

{% endblock %}
```

Nous avons utilisé la méthode `form_row()` pour afficher les champs du formulaire. Cette méthode affiche le label et le champ. Il existe d'autres méthodes pour afficher les champs du formulaire :

- `form_start()` : affiche le tag `<form>` et les attributs du formulaire
- `form_end()` : affiche le tag `</form>`
- `form_widget()` : affiche le champ
- `form_label()` : affiche le label
- `form_errors()` : affiche les erreurs de validation
- `form_rest()` : affiche les champs restants

---

Vous pouvez maintenant créer des formulaires dans vos applications Symfony. Pour en savoir plus sur les formulaires, consultez la [documentation officielle](https://symfony.com/doc/current/forms.html).
