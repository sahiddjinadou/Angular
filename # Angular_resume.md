# Angular

## Présentation des composants

Les composants sont les principaux éléments de base des applications Angular. Chaque composant se compose de :

- Un modèle HTML qui déclare ce qui est rendu sur la page
- Une classe TypeScript qui définit le comportement
- Un sélecteur CSS qui définit comment le composant est utilisé dans un modèle
- En option, styles CSS appliqués au modèle

Cette rubrique décrit comment créer et configurer un composant Angular.

### Conditions préalables

 1. installer le projet Angular Cli : npm install -g @angular/cli@17
 2. creer l'espace de travail : ng new my-app

## Créer un composant

La meilleure façon de créer un composant est d'utiliser Angular CLI. Vous pouvez également créer un composant manuellement.

### Créer un composant à l'aide de l'Angular CLI

1. Depuis une fenêtre de terminal, accédez au répertoire contenant votre application.
2. Exécutez la `ng generate component <component-name>`commande, où `<component-name>`est le nom de votre nouveau composant.

```js
import { Component } from '@angular/core';

@Component({
  selector: 'app-component-overview',
  templateUrl: './component-overview.component.html',
//   styleUrls: ['./component-overview.component.css'],//
  styles: ['h1 { font-weight: normal;color:red; }']
})

export class TaskComponent {

}

```

### Styles de composants

Pour chaque composant Angular que vous écrivez, vous pouvez définir non seulement un modèle HTML, mais également les styles CSS qui vont avec ce modèle, en spécifiant les sélecteurs, les règles et les requêtes multimédias dont vous avez besoin.

Une façon de procéder consiste à définir la stylespropriété dans les métadonnées du composant. La stylespropriété prend un tableau de chaînes contenant du code CSS.  
comme dans l'exemple suivant :  

 ```js
 @Component({
  selector: 'app-root',
  template: `
    <h1>Tour of Heroes</h1>
    <app-hero-main [hero]="hero"></app-hero-main>
  `,
  styles: ['h1 { font-weight: normal; }'] //css
})
export class HeroAppComponent {
/* . . . */
}
 ```

 dans un projet angular tout les composant sont  placés dans le dossier app

 ### Les Événements en Angular

Les événements en Angular jouent un rôle crucial dans la communication entre les composants, la gestion des interactions utilisateur et la réponse aux changements d'état. Voici un aperçu des concepts clés et des cas d'utilisation des événements en Angular.

#### Concepts Clés des Événements en Angular

1. **Événements DOM** :
   - **Définition** : Les événements DOM sont les événements déclenchés par les interactions de l'utilisateur avec les éléments HTML, comme les clics, les saisies clavier, et les mouvements de souris.
   - **Utilisation** : Angular permet de gérer ces événements dans les templates avec la syntaxe `(event)`, par exemple `(click)`, `(input)`, `(mouseover)`, etc.
   
   ```html
   <button (click)="onClick()">Click me</button>
   ```

   ```typescript
   export class MyComponent {
     onClick() {
       console.log('Button clicked');
     }
   }
   ```

2. **Événements Personnalisés** :
   - **Définition** : Les événements personnalisés sont définis par les développeurs pour communiquer des informations entre les composants parent et enfant.
   - **Utilisation** : Utilisez `@Output` et l'objet `EventEmitter` pour créer et émettre des événements personnalisés.

   ```typescript
   import { Component, EventEmitter, Output } from '@angular/core';

   @Component({
     selector: 'child-component',
     template: `<button (click)="sendMessage()">Send Message</button>`
   })
   export class ChildComponent {
     @Output() messageEvent = new EventEmitter<string>();

     sendMessage() {
       this.messageEvent.emit('Hello from Child');
     }
   }
   ```

   ```html
   <child-component (messageEvent)="receiveMessage($event)"></child-component>
   ```

   ```typescript
   export class ParentComponent {
     receiveMessage(message: string) {
       console.log(message);
     }
   }
   ```

3. **Gestion des Événements avec `@HostListener`** :
   - **Définition** : Le décorateur `@HostListener` permet de gérer les événements DOM directement dans la classe du composant.
   - **Utilisation** : Utilisez `@HostListener` pour écouter les événements sur l'hôte du composant.

   ```typescript
   import { Component, HostListener } from '@angular/core';

   @Component({
     selector: 'my-component',
     template: `<p>Resize the window to see the effect</p>`
   })
   export class MyComponent {
     @HostListener('window:resize', ['$event'])
     onResize(event: Event) {
       console.log('Window resized');
     }
   }
   ```

   ## Cas d'Utilisation des Événements

1. **Interaction Utilisateur** :
   - **Exemple** : Capturer l'événement `click` sur un bouton pour déclencher une action.
   
   ```html
   <button (click)="handleClick()">Click me</button>
   ```

   ```typescript
   handleClick() {
     alert('Button clicked!');
   }
   ```

2. **Communication Entre Composants** :
   - **Exemple** : Utiliser des événements personnalisés pour envoyer des données d'un composant enfant à un composant parent.

3. **Formulaires Réactifs** :
   - **Exemple** : Capturer l'événement `submit` d'un formulaire pour valider et envoyer les données.
   
   ```html
   <form (ngSubmit)="onSubmit()" [formGroup]="myForm">
     <input formControlName="name" />
     <button type="submit">Submit</button>
   </form>
   ```

   ```typescript
   onSubmit() {
     console.log(this.myForm.value);
   }
   ```

4. **Événements de Cycle de Vie** :
   - **Exemple** : Utiliser les événements de cycle de vie des composants comme `ngOnInit`, `ngOnChanges`, etc., pour gérer le comportement du composant au cours de sa vie.

   ```typescript
   export class MyComponent implements OnInit {
     ngOnInit() {
       console.log('Component initialized');
     }
   }
   ```

#### Résumé

Les événements en Angular permettent de gérer les interactions utilisateur, de communiquer entre les composants, et de répondre aux changements d'état dans l'application. En utilisant les événements DOM, les événements personnalisés avec `@Output` et `EventEmitter`, et le décorateur `@HostListener`, les développeurs peuvent créer des applications réactives et interactives.

### Questions de Résumé du Cours sur les Événements en Angular

1. **Qu'est-ce qu'un événement DOM en Angular et comment le gérer dans un template ?**
2. **Comment créer et émettre un événement personnalisé dans un composant Angular ?**
3. **Comment utiliser `@HostListener` pour gérer les événements DOM dans la classe d'un composant ?**
4. **Quels sont les cas d'utilisation courants des événements en Angular ?**
5. **Comment les événements personnalisés facilitent-ils la communication entre les composants parent et enfant ?**
6. **Quel est le rôle des événements de cycle de vie dans la gestion des composants Angular ?**

En répondant à ces questions, vous pouvez vérifier la compréhension des concepts et des pratiques liés à la gestion des événements en Angular.

## Le Data Binding Bidirectionnel (Two-Way Binding) en Angular

Le data binding bidirectionnel (two-way binding) en Angular permet de synchroniser les données entre un composant et son template. Cela signifie que les modifications dans le modèle de données sont automatiquement reflétées dans la vue, et vice versa. Cette fonctionnalité est particulièrement utile dans les formulaires où les données de l'utilisateur doivent être synchronisées avec le modèle.

#### Concepts Clés

1. **NgModel Directive** :
   - La directive `ngModel` est utilisée pour implémenter le data binding bidirectionnel.
   - Elle permet de lier une propriété de modèle de données à un élément de formulaire.

2. **Syntaxe de Binding Bidirectionnel** :
   - Utilise la syntaxe `[(ngModel)]` pour lier une propriété de modèle à un élément de formulaire.
   - Les parenthèses `()` indiquent l'écoute des événements, et les crochets `[]` indiquent la liaison de la propriété.

#### Exemple de Base

Voici un exemple simple illustrant le data binding bidirectionnel dans un formulaire.

##### Template

```html
<input [(ngModel)]="name" placeholder="Enter your name">
<p>Hello, {{ name }}!</p>
```

##### Composant

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-name-editor',
  template: `
    <input [(ngModel)]="name" placeholder="Enter your name">
    <p>Hello, {{ name }}!</p>
  `
})
export class NameEditorComponent {
  name: string = '';
}
```

Dans cet exemple, la valeur de l'input est liée à la propriété `name` du composant. Toute modification de l'input met à jour `name`, et toute modification de `name` met à jour l'input.

#### Étapes pour Utiliser `ngModel`

1. **Importer FormsModule** :
   - Assurez-vous d'importer `FormsModule` dans votre module d'application pour utiliser `ngModel`.

   ```typescript
   import { NgModule } from '@angular/core';
   import { BrowserModule } from '@angular/platform-browser';
   import { FormsModule } from '@angular/forms';
   import { AppComponent } from './app.component';
   import { NameEditorComponent } from './name-editor/name-editor.component';

   @NgModule({
     declarations: [
       AppComponent,
       NameEditorComponent
     ],
     imports: [
       BrowserModule,
       FormsModule
     ],
     providers: [],
     bootstrap: [AppComponent]
   })
   export class AppModule { }
   ```

2. **Utiliser `ngModel` dans le Template** :
   - Utilisez la directive `ngModel` pour lier les données dans votre template.

   ```html
   <input [(ngModel)]="name" placeholder="Enter your name">
   ```

3. **Définir la Propriété dans le Composant** :
   - Assurez-vous que la propriété liée existe dans votre composant.

   ```typescript
   export class NameEditorComponent {
     name: string = '';
   }
   ```

#### Cas d'Utilisation Avancés

1. **Formulaires Composés** :
   - Utilisez le data binding bidirectionnel pour gérer des formulaires complexes avec plusieurs champs de saisie.

   ```html
   <form>
     <label for="name">Name:</label>
     <input id="name" [(ngModel)]="user.name" name="name">
     
     <label for="age">Age:</label>
     <input id="age" [(ngModel)]="user.age" name="age" type="number">
     
     <button (click)="submitForm()">Submit</button>
   </form>
   ```

   ```typescript
   export class UserFormComponent {
     user = {
       name: '',
       age: null
     };

     submitForm() {
       console.log(this.user);
     }
   }
   ```

2. **Validation de Formulaires** :
   - Combinez le data binding bidirectionnel avec des validations pour gérer les états de validation de vos formulaires.

   ```html
   <form #form="ngForm">
     <label for="email">Email:</label>
     <input id="email" [(ngModel)]="email" name="email" required email>
     <div *ngIf="form.controls['email']?.invalid && form.controls['email']?.touched">
       Invalid email address
     </div>
     <button [disabled]="form.invalid">Submit</button>
   </form>
   ```

   ```typescript
   export class EmailFormComponent {
     email: string = '';
   }
   ```

### Questions de Résumé du Cours sur le Data Binding Bidirectionnel en Angular

1. **Qu'est-ce que le data binding bidirectionnel en Angular ?**
   - Synchronisation des données entre le modèle de données et la vue.

2. **Quelle directive est utilisée pour le data binding bidirectionnel ?**
   - La directive `ngModel`.

3. **Comment configure-t-on le data binding bidirectionnel dans le template d'un composant ?**
   - Utilisation de la syntaxe `[(ngModel)]`.

4. **Quels modules doivent être importés pour utiliser `ngModel` ?**
   - Le module `FormsModule` doit être importé.

5. **Donnez un exemple de template utilisant le data binding bidirectionnel.**
   - `<input [(ngModel)]="name">`

6. **Comment utiliser le data binding bidirectionnel avec des formulaires complexes ?**
   - Lier chaque champ de saisie à une propriété du modèle de données.

7. **Comment combiner le data binding bidirectionnel avec la validation de formulaires ?**
   - Utiliser les attributs de validation HTML5 et Angular pour gérer les états de validation.

En posant ces questions, vous pouvez évaluer la compréhension des concepts et des pratiques liés au data binding bidirectionnel en Angular.



## Création et Utilisation de Service en Angular

Les services sont des classes en Angular qui contiennent des logiques partagées que vous voulez utiliser dans différentes parties de votre application. Ils permettent de centraliser et réutiliser des fonctionnalités comme l'accès aux données, les communications réseau, ou encore les logiques métiers.  

### Créer un service

Pour créer un service en Angular, vous pouvez utiliser Angular CLI. Par exemple
`ng generate service my-service`

Cela crée deux fichiers : `my-service.service.ts` et `my-service.service.spec.ts`.

```js

import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class MyService {
  constructor() { }

  getHello(): string {
    return 'Hello, World!';
  }
}

```

Le décorateur @Injectable indique qu'Angular peut injecter des dépendances dans cette classe. providedIn: 'root' signifie que le service sera fourni au niveau racine, c'est-à-dire qu'il sera disponible partout dans l'application.

### Utiliser un service dans un composant :  

Pour utiliser ce service dans un composant, il faut l'injecter dans le constructeur du composant.

```js
import { Component, OnInit } from '@angular/core';
import { MyService } from './my-service.service';

@Component({
  selector: 'app-my-component',
  template: '<p>{{ message }}</p>',
})
export class MyComponent implements OnInit {
  message: string;

  constructor(private myService: MyService) { }

  ngOnInit(): void {
    this.message = this.myService.getHello();
  }
}

```

### Compréhension de l'Injection de Dépendances  

__L'injection de dépendances (DI) :__
L'injection de dépendances est un design pattern qui permet de créer des objets et de les fournir à d'autres objets plutôt que de les créer directement. Cela favorise la modularité, la réutilisabilité, et facilite les tests

__Comment ça marche en Angular :__  
En Angular, DI fonctionne en utilisant des "injecteurs". Un injecteur maintient un conteneur de dépendances que les classes peuvent demander. Lorsque Angular instancie une classe qui déclare une dépendance, l'injecteur fournit cette dépendance.

__Exemple d'injection de dépendances :__  Dans l'exemple précédent, nous avons injecté `MyService` dans `MyComponent`.

```js
constructor(private myService: MyService) { }

```

#### Résumé:

- __Services__  : Centralisent et réutilisent des logiques partagées dans l'application.
- __Création__  : Utiliser Angular CLI pour générer des services.
- __Injection__ : Utiliser le décorateur `@Injectable` pour les services et injecter les dépendances via les constructeurs des classes.

## Modules en Angular

Les modules en Angular sont un élément fondamental de l'architecture de l'application. Ils permettent de regrouper des composants, des directives, des services et d'autres fonctionnalités de l'application dans des unités logiques. Cela rend l'application plus modulaire, maintenable et permet le chargement paresseux (lazy loading).

### Types de Modules en Angular

1. __Module Racine (AppModule)__ : C'est le module principal de l'application, généralement défini dans app.module.ts. Il bootstrap l'application et importe d'autres modules nécessaires.

2. __Modules Fonctionnels__ : Ces modules sont créés pour regrouper des fonctionnalités spécifiques de l'application, comme un module pour la gestion des utilisateurs, un module pour les produits, etc.

3. __Modules Partagés (Shared Modules)__ : Utilisés pour regrouper des composants, directives, et pipes qui sont partagés entre plusieurs modules.

4. __Modules de Fonctionnalités (Feature Modules)__ : Utilisés pour organiser des fonctionnalités spécifiques, souvent utilisés avec le chargement paresseux pour optimiser les performances de l'application.

### Structure de Base d'un Module  

Un module Angular est défini en utilisant le décorateur @NgModule. Voici un exemple de module de base :

```js

import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { FormsModule } from '@angular/forms';
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpClientModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

#### Explication des Sections

- __declarations__ : Contient les composants, directives et pipes qui appartiennent à ce module.
- __imports__:Contient d'autres modules que ce module utilise. Par exemple, `BrowserModule` est importé pour les applications web,`FormsModule` pour les formulaires, et `HttpClientModule` pour les requêtes HTTP.
- __providers__ : Contient les services qui doivent être disponibles pour le module.
- __bootstrap__ : Spécifie le composant principal qui doit être bootstrapé lors du démarrage de l'application.

### Création d'un Module

Pour créer un nouveau module, vous pouvez utiliser Angular CLI : `ng generate module my-module`
Cela crée un nouveau fichier de module `my-module.module.ts`

````js
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

@NgModule({
  declarations: [],
  imports: [
    CommonModule
  ]
})
export class MyModule { }

````

### Utilisation des Modules

Pour utiliser un module dans un autre module, il faut l'importer dans la section `imports` 

```js 
 import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { MyModule } from './my-module/my-module.module';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    MyModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

#### Modules Partagés

Les modules partagés contiennent des composants, directives, et pipes réutilisables. Par exemple :

```js
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { SharedComponent } from './shared-component/shared-component.component';

@NgModule({
  declarations: [SharedComponent],
  imports: [CommonModule],
  exports: [SharedComponent]
})
export class SharedModule { }

```

Ensuite, vous pouvez importer `SharedModule` dans d'autres modules pour utiliser `SharedComponent`.

Les modules en Angular permettent de structurer votre application de manière modulaire, facilitant la maintenance et l'extensibilité. Ils permettent également d'optimiser les performances grâce au chargement paresseux.  

## Cas d'utilisation : Module Partagé pour des Composants Communs

Imaginons une application qui possède plusieurs fonctionnalités distinctes, chacune dans son propre module, mais qui partage des composants comme une barre de navigation, un pied de page, et des utilitaires comme des pipes de formatage.

#### Étapes pour créer et utiliser un module partagé

1. Création du Module Partagé :`ng generate module shared` => `shared.module.ts`
2. Ajout de Composants, Directives, et Pipes Communs :  
  `ng generate component shared/navbar`
  `ng generate component shared/footer`
  `ng generate pipe shared/customDate`

3. Définition du Module Partagé
  Dans `shared.module.ts`, déclarez et exportez les composants, directives, et pipes communs.

```js
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { NavbarComponent } from './navbar/navbar.component';
import { FooterComponent } from './footer/footer.component';
import { CustomDatePipe } from './custom-date.pipe';

@NgModule({
  declarations: [
    NavbarComponent,
    FooterComponent,
    CustomDatePipe
  ],
  imports: [
    CommonModule
  ],
  exports: [
    NavbarComponent,
    FooterComponent,
    CustomDatePipe
  ]
})
export class SharedModule { }

```

- __declarations__ : Liste les composants, directives, et pipes que ce module définit.
- __imports__ : Liste les modules dont ce module dépend. `CommonModule` est importé pour avoir accès aux directives Angular communes comme `ngIf` et `ngFor`.
- __exports__ : Liste les composants, directives, et pipes que ce module rend disponibles pour d'autres modules.

4. Utilisation du Module Partagé dans d'autres Modules :  
Importez le module partagé dans d'autres modules où vous avez besoin des composants, directives, ou pipes communs. Par exemple, dans un module de fonctionnalité `FeatureModule` :

```js
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { SharedModule } from '../shared/shared.module';
import { FeatureComponent } from './feature.component';

@NgModule({
  declarations: [
    FeatureComponent
  ],
  imports: [
    CommonModule,
    SharedModule
  ]
})
export class FeatureModule { }

```

Ensuite, vous pouvez utiliser les composants et pipes du module partagé dans les templates de FeatureComponent.

`<app-navbar></app-navbar>`
`<app-feature></app-feature>`
`<app-footer></app-footer>`

5. App Module

Assurez-vous que le module partagé est également importé dans le module racine si nécessaire :

```js
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { SharedModule } from './shared/shared.module';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    SharedModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

Un module partagé permet de centraliser les composants, directives, et pipes communs pour qu'ils puissent être utilisés dans différents modules de l'application. Cela facilite la maintenance et réduit la duplication de code. Dans notre exemple, nous avons créé un module partagé qui contient une barre de navigation, un pied de page, et un pipe de formatage personnalisé, et nous avons montré comment l'utiliser dans un module de fonctionnalité.

Pour résumer le contenu d'un cours sur les modules partagés en Angular, vous pouvez poser les questions suivantes. Ces questions couvrent les concepts clés et les aspects pratiques liés à la création et à l'utilisation des modules partagés.

### Questions de Résumé du Cours

1. **Qu'est-ce qu'un module partagé en Angular ?**
   - Un module partagé regroupe des composants, des directives, des pipes, et des services qui sont réutilisés dans plusieurs modules de l'application.

2. **Pourquoi utiliser des modules partagés dans une application Angular ?**
   - Pour centraliser les éléments communs et éviter la duplication de code, facilitant ainsi la maintenance et la modularité de l'application.

3. **Comment crée-t-on un module partagé en Angular ?**
   - Utilisez Angular CLI pour générer un module : `ng generate module shared`.

4. **Quels types de composants sont généralement inclus dans un module partagé ?**
   - Des composants réutilisables comme une barre de navigation, un pied de page, des directives personnalisées, et des pipes.

5. **Comment déclare-t-on et exporte-t-on des composants dans un module partagé ?**
   - Utilisez les sections `declarations` et `exports` dans le décorateur `@NgModule` pour déclarer et exporter les composants, directives et pipes.

6. **Comment utilise-t-on un module partagé dans un autre module ?**
   - Importez le module partagé dans la section `imports` du module où vous avez besoin des composants partagés.

7. **Quels sont les avantages de centraliser les services dans un module partagé ?**
   - Les services centralisés permettent une gestion cohérente des données et des fonctionnalités partagées à travers toute l'application.

8. **Comment configure-t-on un module partagé pour être utilisé à travers toute l'application ?**
   - Assurez-vous que le module partagé est importé dans le module racine (AppModule) si ses composants ou services doivent être disponibles globalement.

9. **Qu'est-ce que le chargement paresseux (lazy loading) et comment est-il lié aux modules partagés ?**
   - Le chargement paresseux permet de charger les modules uniquement quand cela est nécessaire, optimisant ainsi les performances. Les modules partagés peuvent être utilisés dans les modules chargés paresseusement pour réutiliser des composants ou services communs.

10. **Quels sont les pièges courants à éviter lors de l'utilisation de modules partagés ?**
    - Évitez d'inclure des services spécifiques aux fonctionnalités dans le module partagé, car cela peut créer des dépendances circulaires et compliquer le débogage. Gardez les modules partagés aussi génériques que possible.

### Résumé

Ces questions permettent de vérifier la compréhension des concepts fondamentaux relatifs aux modules partagés en Angular, leur création, leur utilisation, et leurs avantages. Elles aident également à mettre en lumière les meilleures pratiques et les pièges courants à éviter.


Le **Routing** en Angular permet de naviguer entre différentes vues ou composants au sein d'une application de manière fluide et intuitive, en modifiant l'URL du navigateur. Voici une vue d'ensemble sur le fonctionnement du routing en Angular et les étapes pour le mettre en place.

### Concepts Clés du Routing en Angular

1. **RouterModule** : 
   - Module d'Angular qui permet de configurer et gérer le routage dans l'application.
   - Il fournit des services, des directives et des classes nécessaires pour le routage.

2. **Routes** :
   - Configuration des chemins d'URL et des composants associés.
   - Chaque route est un objet avec des propriétés comme `path` et `component`.

3. **RouterOutlet** :
   - Directive qui agit comme un espace réservé où les vues des composants correspondants aux routes définies seront rendues.

4. **RouterLink** :
   - Directive pour créer des liens de navigation.

### Étapes pour Configurer le Routing en Angular

#### 1. Configurer les Routes

Définir les routes dans un module de routage (souvent appelé `AppRoutingModule`).

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
import { PageNotFoundComponent } from './page-not-found/page-not-found.component';

const routes: Routes = [
  { path: '', redirectTo: '/home', pathMatch: 'full' },
  { path: 'home', component: HomeComponent },
  { path: 'about', component: AboutComponent },
  { path: '**', component: PageNotFoundComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

#### 2. Ajouter `RouterOutlet` dans le Template

Ajouter `<router-outlet>` dans le template principal (souvent `AppComponent`) pour indiquer où afficher les composants routés.

```html
<router-outlet></router-outlet>
```

#### 3. Utiliser `RouterLink` pour la Navigation

Utiliser la directive `routerLink` pour créer des liens de navigation.

```html
<nav>
  <a routerLink="/home">Home</a>
  <a routerLink="/about">About</a>
</nav>
```

#### 4. Importer `AppRoutingModule` dans `AppModule`

Assurez-vous d'importer et de déclarer `AppRoutingModule` dans le module principal de l'application (`AppModule`).

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
import { PageNotFoundComponent } from './page-not-found/page-not-found.component';

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    AboutComponent,
    PageNotFoundComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### Cas d'Utilisation Avancés

#### 1. Routes Enfant (Nested Routes)

Vous pouvez avoir des routes enfant pour gérer des vues imbriquées.

```typescript
const routes: Routes = [
  {
    path: 'dashboard',
    component: DashboardComponent,
    children: [
      { path: 'statistics', component: StatisticsComponent },
      { path: 'reports', component: ReportsComponent }
    ]
  }
];
```

#### 2. Paramètres de Route

Pour passer des paramètres dans l'URL, utilisez `:param`.

```typescript
const routes: Routes = [
  { path: 'user/:id', component: UserComponent }
];
```

Pour accéder aux paramètres dans le composant :

```typescript
import { ActivatedRoute } from '@angular/router';

export class UserComponent {
  constructor(private route: ActivatedRoute) {
    this.route.params.subscribe(params => {
      console.log(params['id']);
    });
  }
}
```
Pour récupérer le paramètre `id` d'une URL dans un composant Angular, vous pouvez utiliser le service `ActivatedRoute`. Ce service permet d'accéder aux informations de la route active, y compris les paramètres de route. Voici comment procéder :

### Étapes pour Récupérer le Paramètre `id`

1. **Définir la Route** :
   - Comme vous l'avez déjà fait, définissez une route avec un paramètre dynamique `id` :
   ```typescript
   const routes: Routes = [
     { path: 'user/:id', component: UserComponent }
   ];
   ```

2. **Injecter `ActivatedRoute` dans le Composant** :
   - Dans le composant `UserComponent`, vous allez injecter `ActivatedRoute` pour accéder aux paramètres de route.

3. **Récupérer le Paramètre `id`** :
   - Utilisez `this.route.snapshot.paramMap.get('id')` pour obtenir la valeur du paramètre `id` au moment où le composant est initialisé.
   - Ou utilisez `this.route.paramMap.subscribe(params => ...)` pour écouter les changements de paramètres de route (utile si le composant reste chargé et que seul l'ID change).

### Exemple Complet

Voici un exemple de comment faire cela dans le composant `UserComponent` :

```typescript
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html'
})
export class UserComponent implements OnInit {
  userId!: string;  // Ou number, selon votre logique

  constructor(private route: ActivatedRoute) { }

  ngOnInit(): void {
    // Méthode 1 : Récupérer le paramètre ID une seule fois lors de l'initialisation
    this.userId = this.route.snapshot.paramMap.get('id') || '';

    // Méthode 2 : S'abonner aux changements de paramètre ID (utile si le paramètre peut changer sans rechargement du composant)
    this.route.paramMap.subscribe(params => {
      this.userId = params.get('id') || '';
    });
  }
}
```

### Explication des Méthodes

1. **Méthode 1 : `this.route.snapshot.paramMap.get('id')`** :
   - Utilisez cette méthode pour obtenir le paramètre `id` lors de l'initialisation du composant.
   - C'est pratique si le paramètre ne changera pas tant que le composant est chargé.

2. **Méthode 2 : `this.route.paramMap.subscribe(params => {...})`** :
   - Utilisez cette méthode pour vous abonner aux changements de paramètres. Si l'ID change mais que le composant reste chargé, cette méthode garantit que vous obtenez toujours la valeur la plus à jour.
   - Cette approche est utile dans des scénarios où le composant `UserComponent` pourrait être réutilisé pour afficher différents utilisateurs sans être détruit et recréé à chaque changement d'ID.






#### 3. Guards (Garde de Route)

Pour protéger les routes, utilisez des guards comme `CanActivate`.

```typescript
import { Injectable } from '@angular/core';
import { CanActivate, Router } from '@angular/router';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {
  constructor(private router: Router) {}

  canActivate(): boolean {
    const isAuthenticated = // logique d'authentification
    if (!isAuthenticated) {
      this.router.navigate(['/login']);
      return false;
    }
    return true;
  }
}
```

Et configurez la route avec le guard :

```typescript
const routes: Routes = [
  { path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] }
];
```




### Questions de Résumé du Cours sur le Routing en Angular

1. **Qu'est-ce que le `RouterModule` et quel est son rôle dans Angular ?**
2. **Comment définir une route de base dans Angular ?**
3. **À quoi sert la directive `<router-outlet>` dans Angular ?**
4. **Comment créer un lien de navigation avec `routerLink` ?**
5. **Comment configurer des routes enfants (nested routes) dans Angular ?**
6. **Comment passer et accéder à des paramètres de route dans Angular ?**
7. **Qu'est-ce qu'un guard et comment l'utiliser pour protéger des routes ?**
8. **Comment rediriger une route par défaut dans Angular ?**
9. **Comment gérer une route non trouvée (404) avec Angular ?**
10. **Quels sont les avantages d'utiliser le routing dans une application Angular ?**

En répondant à ces questions, vous pouvez vérifier la compréhension des concepts et des pratiques liés au routing en Angular.
Ajouter une communication HTTP à une application Angular implique généralement l'utilisation du service `HttpClient`, qui fait partie du module `HttpClientModule` d'Angular. Ce service permet d'envoyer des requêtes HTTP pour interagir avec une API backend (par exemple, pour récupérer des données, envoyer des informations, etc.).

### Étapes pour Ajouter une Communication HTTP

1. **Importer `HttpClientModule` dans votre Module Principal** :
   - Le module `HttpClientModule` doit être importé dans le module principal de votre application (souvent `AppModule`).

   ```typescript
   import { BrowserModule } from '@angular/platform-browser';
   import { NgModule } from '@angular/core';
   import { HttpClientModule } from '@angular/common/http';
   import { AppComponent } from './app.component';

   @NgModule({
     declarations: [
       AppComponent,
       // Autres composants
     ],
     imports: [
       BrowserModule,
       HttpClientModule, // Import du module HttpClient
       // Autres modules
     ],
     providers: [],
     bootstrap: [AppComponent]
   })
   export class AppModule { }
   ```

2. **Créer un Service pour Gérer les Requêtes HTTP** :
   - Créez un service Angular pour centraliser la gestion des requêtes HTTP.

   ```typescript
   import { Injectable } from '@angular/core';
   import { HttpClient } from '@angular/common/http';
   import { Observable } from 'rxjs';

   @Injectable({
     providedIn: 'root'
   })
   export class UserService {

     private apiUrl = 'https://api.example.com/users';  // Remplacez par votre API

     constructor(private http: HttpClient) { }

     // Méthode pour obtenir tous les utilisateurs
     getUsers(): Observable<any> {
       return this.http.get(this.apiUrl);
     }

     // Méthode pour obtenir un utilisateur par ID
     getUserById(id: string): Observable<any> {
       return this.http.get(`${this.apiUrl}/${id}`);
     }

     // Méthode pour créer un nouvel utilisateur
     createUser(user: any): Observable<any> {
       return this.http.post(this.apiUrl, user);
     }

     // Méthode pour mettre à jour un utilisateur
     updateUser(id: string, user: any): Observable<any> {
       return this.http.put(`${this.apiUrl}/${id}`, user);
     }

     // Méthode pour supprimer un utilisateur
     deleteUser(id: string): Observable<any> {
       return this.http.delete(`${this.apiUrl}/${id}`);
     }
   }
   ```

3. **Utiliser le Service dans un Composant** :
   - Injectez le service dans un composant pour l'utiliser et interagir avec l'API.

   ```typescript
   import { Component, OnInit } from '@angular/core';
   import { UserService } from './user.service';

   @Component({
     selector: 'app-user-list',
     template: `
       <h2>Liste des Utilisateurs</h2>
       <ul>
         <li *ngFor="let user of users">
           {{ user.name }} ({{ user.email }})
         </li>
       </ul>
     `
   })
   export class UserListComponent implements OnInit {

     users: any[] = [];

     constructor(private userService: UserService) { }

     ngOnInit(): void {
       this.userService.getUsers().subscribe(data => {
         this.users = data;
       });
     }
   }
   ```

4. **Gérer les Erreurs HTTP** :
   - Il est important de gérer les erreurs lors des requêtes HTTP. Utilisez `catchError` pour capturer les erreurs.

   ```typescript
   import { catchError } from 'rxjs/operators';
   import { throwError } from 'rxjs';

   getUsers(): Observable<any> {
     return this.http.get(this.apiUrl).pipe(
       catchError(this.handleError)
     );
   }

   private handleError(error: any) {
     console.error('An error occurred', error);
     return throwError('Something went wrong; please try again later.');
   }
   ```

### Explications et Bonnes Pratiques

- **Centralisation dans un Service** : La logique de communication HTTP est centralisée dans un service (`UserService` dans l'exemple), ce qui rend le code plus modulaire et plus facile à maintenir.
- **Gestion des Erreurs** : En utilisant `catchError`, vous pouvez gérer les erreurs de manière cohérente, ce qui est crucial pour une application robuste.
- **Observable** : Le service `HttpClient` retourne des `Observable`, ce qui permet de gérer de manière asynchrone les réponses HTTP. Vous pouvez utiliser `subscribe` pour vous abonner aux résultats des requêtes.

### Conclusion

En ajoutant une communication HTTP via `HttpClient` à votre application Angular, vous pouvez interagir efficacement avec des API backend pour récupérer ou envoyer des données, améliorant ainsi les fonctionnalités de votre application. Les services jouent un rôle crucial dans la gestion de cette communication, en maintenant la séparation des préoccupations et en facilitant la réutilisation du code.

# Refference

https://angular.dev/guide/templates/class-binding
https://jsonplaceholder.typicode.com/users

