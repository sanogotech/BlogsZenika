---
ID: 461
post_title: 'AngularJS : Les directives'
author: mlux
post_date: 2013-12-19 10:00:00
post_excerpt: '<p>Les directives d’AngularJS sont à la fois la grande force et le point difficile à maîtriser quand on aborde le framework. De nombreux articles ont déjà abordé le sujet de la création de directives, le plus souvent en détaillant l’API, mais je trouve que cela ne répond pas aux vraies questions que l’on se pose en abordant le sujet. Ces questions que je me suis moi-même posée sont les suivantes&nbsp;:</p> <ul> <li>Que représente exactement le concept de directive dans AngularJS&nbsp;?</li> <li>Quand écrire une directive&nbsp;?</li> <li>Comment gérer le scope et les bindings dans une directive&nbsp;?</li> <li>Est-il possible de coopérer avec ngModel&nbsp;?</li> <li>Qu’est ce que la transclusion&nbsp;?</li> </ul>'
layout: post
permalink: http://blog.zenika-offres.com/?p=461
published: true
slide_template:
  - ""
---
<p>Les directives d’AngularJS sont à la fois la grande force et le point difficile à maîtriser quand on aborde le framework. De nombreux articles ont déjà abordé le sujet de la création de directives, le plus souvent en détaillant l’API, mais je trouve que cela ne répond pas aux vraies questions que l’on se pose en abordant le sujet. Ces questions que je me suis moi-même posée sont les suivantes&nbsp;:</p> <ul> <li>Que représente exactement le concept de directive dans AngularJS&nbsp;?</li> <li>Quand écrire une directive&nbsp;?</li> <li>Comment gérer le scope et les bindings dans une directive&nbsp;?</li> <li>Est-il possible de coopérer avec ngModel&nbsp;?</li> <li>Qu’est ce que la transclusion&nbsp;?</li> </ul>
<!--more-->
<h4>Directive&nbsp;: la définition</h4> <p>Tout d’abord, les directives ne sont pas des composants ou des widgets, ou du moins, pas seulement. J’ai lu à de trop nombreuses reprises cette simplification dangereuse.</p> <p>La définition la plus propre que je pourrais trouver est de dire qu’il s’agit d’un comportement associé à un trigger dans le DOM. J’aime faire l’analogie avec jQuery&nbsp;: jQuery sélectionne un ensemble d’éléments pour leur affecter une modification. Avec Angular et donc les directives, on inverse le mécanisme en définissant en amont un comportement qu’on active en écrivant le code HTML.</p> <p>Ce fameux déclencheur est le plus souvent un attribut HTML spécifique (ng-repeat, ng-click…) mais les directives d’Angular peuvent être déclenchées de plusieurs façons&nbsp;: balise, attribut, classe et même récemment&nbsp;: commentaire.</p> <p>Ce qu’il faut bien comprendre est que l’intégralité du langage de template d’Angular n’est rien d’autre qu’un ensemble de directives de base qui a été implémenté avec exactement la même API que celle qu’on étudie ici. Il est tout à fait possible, voire même conseillé, d’en consulter les sources ici&nbsp;: <a href="https://github.com/angular/angular.js/tree/master/src/ng/directive" title="https://github.com/angular/angular.js/tree/master/src/ng/directive">https://github.com/angular/angular....</a>. Certaines sont très faciles d’accès et permettent de se faire une bonne idée de comment Angular fonctionne, comme <a href="https://github.com/angular/angular.js/blob/master/src/ng/directive/ngBind.js">ng-bind</a>. D’autres sont un peu moins avenantes, par exemple <a href="https://github.com/angular/angular.js/blob/master/src/ng/directive/ngRepeat.js">ng-reapeat</a>.</p> <p>Comme énoncé en introduction, je ne m’engagerai pas à détailler chaque option de l’API. La seule chose qu’il faut vraiment savoir sur l’API c’est que la documentation se trouve de façon peut être sensée, mais pas très naturelle ici&nbsp;: <a href="http://docs.angularjs.org/api/ng.$compile" title="http://docs.angularjs.org/api/ng.$compile">http://docs.angularjs.org/api/ng.$c...</a>. D’autant qu’en plus, elle a récemment changé d’emplacement.</p> <p>Les propriétés les plus simples permettent de définir le nom de la directive, si elle réagit aux balises ou aux propriétés ou encore s’il faut remplacer le contenu de la balise par un template. Les autres seront un peu plus difficiles d’accès avec des fonctions à définir pour ajouter du comportement, la manipulation du scope ou encore la transclusion.</p> <h4>Applications des directives</h4> <p>Avant d’aller plus loin sur les mécanismes, il faut réussir à se projeter correctement sur les différents cas d’utilisation des directives. Ainsi en étudiant les possibilités, il sera possible de se projeter sur leurs mises en pratique. Voici quelques cas pratiques d’utilisation sans pour autant en faire une liste exhaustive.</p> <h5>Binding</h5> <p>Le premier cas auquel il faut penser est la réalisation d’un binding. Si Angular possède un mécanisme interne assez complexe de dirty checking du scope (que je ne détaillerais pas ici), il ne se passerait rien dans la page à proprement parler s’il n’y avait pas une directive pour faire le lien entre les modifications du scope et la mise en oeuvre dans la page. L’exemple le plus typique est la directive <a href="https://github.com/angular/angular.js/blob/master/src/ng/directive/ngBind.js">ngBind</a> dont j’ai déjà parlé et qui réalise justement ce travail. Elle est intéressante à étudier, car lors de la réalisation de nouvelles directives, on est souvent amené à justement avoir la responsabilité de recréer ce genre de binding.</p> <h5>Mise en forme</h5> <p>D’autres directives apparentées au binding sont celles qui pilotent le style de la page. Parmi les directives de base d’Angular, on parlera d’<a href="https://github.com/angular/angular.js/blob/master/src/ng/directive/ngClass.js">ngClass</a>, d’<a href="https://github.com/angular/angular.js/blob/master/src/ng/directive/ngStyle.js">ngStyle</a> ou encore d’<a href="https://github.com/angular/angular.js/blob/master/src/ng/directive/ngShowHide.js">ngShow / ngHide</a>. Elles opèrent le même type de binding que pour le contenu, mais pour piloter des options de style qui font évoluer la mise en forme de la page.</p> <h5>Flow</h5> <p>Les directives ont pour objectif de créer un langage de templating complet donc il faut encore ajouter la catégorie des directives pilotant le flow de construction du DOM. La directive la plus représentative de cette catégorie est bien sûr <a href="https://github.com/angular/angular.js/blob/master/src/ng/directive/ngRepeat.js">ngRepeat</a>. Ces directives font appel à la transclusion qui est traitée plus loin dans cet article.</p> <h5>Widgets</h5> <p>Enfin, je termine par la catégorie qui a tendance à monopoliser l’attention sur les directives à savoir les Widgets. Il est effectivement possible de construire une directive suffisamment conséquente pour qu’elle génère automatiquement un widget entier et configurable. Attention toutefois aux widgets trop riches. Elles perdent alors en réutilisabilité. Il faut aussi noter que pour la construction de widgets, il sera assez courant de créer plusieurs directives pour un seul widget. Chaque directive de l’ensemble coopérant pour construire le fonctionnel souhaité.</p> <h4>Cycle de vie</h4> <p>AngularJS propose un service <a href="http://docs.angularjs.org/api/ng.$compile">compiler</a> qui a la responsabilité de “compiler” le DOM pour en interpréter les directives. Ce compilateur travaille sur le DOM et interprète les directives successivement en respectant l'arborescence du DOM.</p> <p>En écrivant une directive, il est possible d’intervenir à plusieurs étapes de la compilation afin de rendre toutes les transformations possibles, c’est ce que j’ai appelé ici cycle de vie (ce n’est pas un terme qu’on retrouve directement dans la documentation).</p> <p>En pratique, intervenir dans le cycle de vie de la directive revient à définir une fonction ou une autre dans l’objet de configuration de la directive. Le cas le plus courant est d’utiliser la fonction link. La fonction link est appelée lorsque la plupart des choses sont prêtes et qu’on souhaite alors ajouter du comportement telles que des handlers d’évènements ou une surveillance du scope.</p> <h5>Compile</h5> <p>Plus généralement, il y a plus d’étapes auxquelles il est possible d’intervenir. La toute première est l’étape de compilation qui a lieu avant la compilation du contenu de la balise où se trouve la directive. C’est très utile dans les cas ou l’on souhaite intervenir sur le template de la directive avant de l’interpréter.</p> <h5>Controller</h5> <p>Le contrôleur ensuite. Une directive peut avoir un contrôleur. Attention c’est très perturbant, car il s’agit d’un concept ressemblant aux contrôleurs d’Angular sans pour autant être la même chose. Le contrôleur est exécuté avant que le rendu du contenu de la directive soit interprété, ce n’est donc pas là qu'il faut ajouter des handlers sur le contenu. Par contre, le contrôleur a une particularité importante&nbsp;: il peut être récupéré depuis une autre directive. Par le jeu des dépendances entre directives, une directive pourra récupérer ce contrôleur ce qui permet de créer une communication et une coopération entre les directives.</p> <h5>Link</h5> <p>Enfin, les fonctions pre-link et post-link interviennent juste avant et juste après la compilation du contenu de la balise qui contient la directive. On utilise le plus souvent la fonction post-link pour réaliser la majorité des opérations puisqu’elle a lieu une fois que le contenu est prêt et qu’il est donc disponible pour agir dessus.</p> <p>Une des étapes déconcertante pour définir les fonctions de link est qu’il y a plusieurs façons de le faire, mais il s’agit bien toujours de la définiti
on des mêmes méthodes. Voici sous forme de code ces différentes écritures.</p> <pre> 	//Méthode la plus directe, on ne passe même pas par l’objet de définition de la directive 	myModule.directive(‘myDirective’, function() { 		return function postLink() { … } 	}); 	//Solution souvent suffisante 	myModule.directive(‘myDirective’, function() { 		return { 			link: function postLink() { … } 		} 	}); 	//Avec la spécialisation pre et post 	myModule.directive(‘myDirective’, function() { 		return { 			link: { 				pre: function preLink() { … }, 				post: function postLink() { … } 			} 		} 	}); 	//Via la compilation 	myModule.directive(‘myDirective’, function() { 		return { 			compile: function() { 				... 				return function postLink() { … }; 			} 		} 	}); 	//La totale 	myModule.directive(‘myDirective’, function() { 		return { 			compile: function() { 				... 				return { 					pre: function preLink() { … }, 					post: function postLink() { … } 				} 			} 		} 	}); </pre> <h4>Scope &amp; Binding</h4> <p>Se lancer dans la rédaction de directives amène rapidement à comprendre les scopes et les bindings de façon plus précise. Ayant pour objectif de me focaliser ici sur les directives, je ne reprends pas les principes de création et héritages des scopes d’Angular.</p> <p>La propriété <strong>scope</strong> de la définition de la directive est fondatrice de la relation de la directive avec le scope. Trois fonctionnements de bases sont possibles.</p> <h5>scope: false (par défaut) ou "pas de scope"</h5> <p>Ce fonctionnement implique que la directive ne crée aucun scope et évolue dans le scope où elle se trouve. Le risque de ce fonctionnement est que la directive modifie le scope où elle se trouve ce qui est rarement le fonctionnement souhaité.</p> <p>Je n’ai jamais vu et ne m’attends pas à ce qu’une directive modifie le contenue du scope sauf saisie de l’utilisateur. Le bon cas d’utilisation de cette possibilité concerne les directives qui ne font que lire le scope, ainsi, on ne crée pas de scope pour la directive et on économise de la mémoire.</p> <h5>scope:{} ou "création d’un scope isolé"</h5> <p>Cette solution est assez particulière et pourtant c’est elle que la documentation incite à utiliser. Il n’est pas explicitement marqué de l’utiliser de préférence, mais comme la documentation est plus complète, on a l’impression que c’est elle qu'il faut utiliser.</p> <p>On parle donc ici d’un scope isolé. Cela veut donc dire qu’un scope sera créé pour la directive, mais ce scope n’héritera pas directement du scope courant. Il est toujours possible d’accéder au scope courant avec la propriété $parent, mais pas par le système de prototype habituel.</p> <p>Ce mécanisme sert, comme son nom l’indique, à faciliter l’isolement de la directive. Il est appuyé par cette fameuse syntaxe qui est si perturbante quand on débute avec les directives qui sert à créer des raccourcis pour ajouter des propriétés spéciales dans ce fameux scope isolé. Comme je l’avais précisé, je ne reproduirais pas ici la documentation officielle, si vous voulez les détails sur cette syntaxe, reportez vous à la <a href="http://docs.angularjs.org/api/ng.$compile#description_comprehensive-directive-api_directive-definition-object">documentation</a>.</p> <p>Ce que je peux préciser par contre c’est qu’il ne faut jamais oublier que cette syntaxe ne représente que des raccourcis sur des mécanismes qu’il est possible de reproduire sans (principalement avec des <a href="http://docs.angularjs.org/api/ng.$parse">$parse</a> et des <a href="http://docs.angularjs.org/api/ng.$rootScope.Scope#methods_$watch">$watch</a>).</p> <p><strong>Cette solution a par contre une sérieuse limitation</strong>. Le fait de créer un scope isolé signifie que tous les scopes en dessous de celui ci, et donc le scope associé à toutes les directives aux éléments du DOM en dessous de la directive courante, seront coupés de l’arbre des scopes. De ce fait, cette solution est pratiquement impossible à utiliser pour une directive qui n’est pas “finale”. Par finale, on entend une directive qui s’applique à un élément qui n’a pas d’enfant dans le DOM.</p> <h5>scope: true ou "création de scope"</h5> <p>Dans ce cas, on crée réellement un nouveau scope avec les mêmes mécanismes qu’un scope créé pour un contrôleur par exemple. Les mécanismes d’héritages fonctionnent alors normalement et si le DOM continue en dessous de l'élément courant, la plupart des bindings continueront de fonctionner correctement.</p> <p>Le problème de risque de modification du scope réapparaît comme dans le cas sans scope. En effet, il est assez facile de modifier le scope parent par inadvertance en choisissant une propriété déjà définie dans le scope parent.</p> <p>Enfin, cette solution ne propose pas les raccourcis proposés dans les scopes isolés. Cela ne veut pas dire que reproduire les mêmes fonctionnalités ne seront pas possible, mais il faudra "le faire à la main".</p> <h4>ngModel</h4> <p>Quand on crée des directives, on arrive très souvent dans le cas d’une directive qui pilote une saisie utilisateur. Hors ce principe est déjà centralisé dans une directive existante&nbsp;: [ngModel|http://docs.angularjs.org/api/ng.directive:ngModel|.</p> <p>Son fonctionnement est assez particulier et demande à être bien compris pour pouvoir intégrer au mieux sa directive. En fait, la directive ngModel ne fait pratiquement rien en elle-même mais elle publie un contrôleur appelé ngModelController qui permettra ensuite à chaque type d’élément de saisie de profiter des mêmes fonctionnalités pour communiquer avec le scope.</p> <p>En pratique, les directives qui utilisent ce contrôleur et réalisent réellement le binding avec l’élément HTML sont déclenchées sur les balises input, select et textarea elles-mêmes.</p> <p>Lorsqu’on souhaite réaliser une directive qui réalise une saisie utilisateur, la bonne pratique est donc de créer une directive qui dépend d’ngModel, d’en récupérer le controller et d’utiliser ses fonctionnalités pour réaliser le binding au model plutôt que de le faire à la main.</p> <p>Pour l’API complète, se référer à la documentation officielle&nbsp;: <a href="http://docs.angularjs.org/api/ng.directive:ngModel.NgModelController" title="http://docs.angularjs.org/api/ng.directive:ngModel.NgModelController">http://docs.angularjs.org/api/ng.di...</a>. On peut résumer les fonctionnalités offertes par le ngModelController en deux grandes catégories.</p> <h5>Transformations</h5> <p>Ce premier rôle consiste à organiser les transformations à réaliser entre le model et la vue et inversement. Il y a le plus souvent des différences entre la représentation de la donnée dans la vue et dans le modèle, l’exemple le plus parlant est celui d’un date picker. Dans la vue, la date sera formatée selon un modèle lisible pour l’utilisateur, mais on s’attend à trouver un objet Date JavaScript dans le modèle. Il faut donc réaliser des transformations pour passer de l’un à l’autre. ngModelController permet de manipuler une liste de "$parsers" et une autre de "$formatters" pour réaliser ces transformations. Il publie ensuite des vues "$viewValue" et "$modelValue" qui sont automatiquement renseignées après la mise en oeuvre des transformations.</p> <p>Exemple (du site officiel) de code d’une directive de saisie utilisant ngModelController&nbsp;:</p> <pre> 	angular.module('customControl', []). 		directive('contenteditable', function() { 			return { 				restrict: 'A', // only activate on element attribute 				require: '?ngModel', // get a hold of NgModelController 				link: function(scope, element, attrs, ngModel) { 					if(!ngModel) return; // do nothing if no ng-model 				// Specify how UI should be updated 				ngModel.$render = function() { 					element.html(ngModel.$viewValue || ''); 				}; 				// Listen for change events to enable binding 				element.on('blur keyup change', function() { 					scope.$apply(read);
}); 				read(); // initialize 				// Write data to the model 				function read() { 					var html = element.html(); 					// When we clear the content editable the browser leaves a &lt;br&gt; behind 					// If strip-br attribute is provided then we strip this out 					if( attrs.stripBr &amp;&amp; html == '&lt;br&gt;' ) { 						html = ''; 					} 					ngModel.$setViewValue(html); 				} 			} 		}; 	}); </pre> <h5>Validations</h5> <p>ngModelController propose également de mettre en oeuvre le système de validation de formulaire standard d’Angular. En utilisant la méthode $setValidity, on pilote tout le mécanisme de validité en indiquant si oui ou non le champ est actuellement valide. L’avantage est que toutes les changements du modèle de données de validité du formulaire sera alors mis à jour automatiquement.</p> <h5>FormController</h5> <p>En parlant du ngModelController, on en arrive à découvrir le FormController qui de façon assez semblable propose un controller qu’il est possible de récupérer pour piloter les mécanismes de validité du formulaire dans son ensemble.</p> <p><a href="http://docs.angularjs.org/api/ng.directive:form.FormController" title="http://docs.angularjs.org/api/ng.directive:form.FormController">http://docs.angularjs.org/api/ng.di...</a></p> <p>Il permet de positionner manuellement les états pristine et dirty et également d’ajouter des contrôles qui pourront ensuite être valides ou non.</p> <p>Si on manipule rarement ce controller directement, il peut être intéressant pour comprendre comment le ngModelController va publier son état au niveau de la validation globale du formulaire.</p> <h4>Transclusion</h4> <p>On en arrive finalement à la dernière notion importante des directives&nbsp;: la transclusion. Tout d’abord, coupon court à tout débat littéraire&nbsp;: ce mot n’existe pas, même pas en anglais, tout juste dans le jargon informatique&nbsp;: <a href="http://en.wikipedia.org/wiki/Transclusion">Transclusion</a>. <em>La transclusion est l’inclusion d’un document ou d’une partie dans un autre par référence</em>. Normalement, à ce niveau, cela ne vous avance pas, mais cela va finir par trouver du sens.</p> <p>La transclusion trouve son sens pour les directives s’appliquant à des éléments du DOM qui n'ont pas de noeuds enfants. Dans ce cas, si la directive ne transforme pas le contenu du DOM en dessous d’elle, il n’y a pas de problème. Si par contre, elle doit réaliser des modifications, elle a besoin de <strong>capturer son contenu avant transformation</strong> pour pouvoir ensuite s’en resservir. C’est ce concept qu’on appelle transclusion. Notez que cette problématique existe exactement de la même façon avec les WebComponents et qu’on a donc pas fini d’en parler même si le terme transclusion ne restera pas forcément.</p> <p>À partir de là, j’ai tendance à distinguer deux utilisations de la transclusion. La première, très simple, peut être mis en oeuvre très rapidement. La seconde demande un peu plus d’investissement.</p> <h5>ngTransclude</h5> <p>Avant toute transclusion, il faut que la directive définisse dans sa configuration <strong>transclude: true</strong>, mais une fois qu’on a fait ça, il ne se passe encore rien.</p> <p>La façon la plus simple d’utiliser la transclusion est d’utiliser la directive ng-transclude. C’est une directive assez particulière puisqu’elle ne fonctionne que dans le cadre d’un template de directive. Elle permet en fait d'indiquer dans votre template que c’est dans cet élément du DOM que vous voulez que soit reproduit le contenu qui a été capturé. Tout le reste sera réalisé pour vous. Voici l’exemple de code officiel qui illustre très bien ce mécanisme&nbsp;:</p> <p>HTML&nbsp;:</p> <pre> 	&lt;pane title=&quot;{{title}}&quot;&gt;{{text}}&lt;/pane&gt; </pre> <p>JavaScript&nbsp;:</p> <pre> 	.directive('pane', function(){ 		return { 			restrict: 'E', 			transclude: true, 			scope: { title:'@' }, 			template: '&lt;div style=&quot;border: 1px solid black;&quot;&gt;' 				+ '&lt;div style=&quot;background-color: gray&quot;&gt;{{title}}&lt;/div&gt;' 				+ '&lt;div ng-transclude&gt;&lt;/div&gt;' + '&lt;/div&gt;' 		}; 	}); </pre> <h5>$transclude function</h5> <p>Vous vous doutez bien que s’il existe une solution plus difficile, c’est que la première solution ne permet pas de traiter tous les cas.</p> <p>Le cas d’école qui nous positionne dans ce cas plus complexe est la directive ng-repeat. En effet, ng-repeat réalise bien une transclusion puisque ce que nous plaçons à l’intérieur est reproduit. Par contre, ce contenu capturé n’est pas juste déplacé, il est également reproduit et associé à un scope différent à chaque itération.</p> <p>Pour répondre à ce genre de besoin, il est possible de réaliser une transclusion de façon bien plus “manuelle”. Il est possible d’obtenir une fonction $transclude dans le controller d’une directive. L’API est très mal documentée, mais cette fonction doit être appelée avec un scope et un callback. Le callback sera alors appelé avec en paramètre, le clone du DOM compilé avec le scope qui a été passé en paramètre. Dans ce callback, nous avons alors la charge d’insérer cet élément où bon nous semble.</p> <p>Si ce n’est pas facile à écrire, on commence tout de même à envisager comment fonctionne ng-repeat&nbsp;: il capture son contenu, surveille la collection sur laquelle il doit itérer. Lors des changements de cette variable, il itère sur chaque élément, crée un nouveau scope dans lequel il positionne la valeur courante de l’iterateur et insère le contenu capturé.</p> <p>Pour illustrer ce discours, voici un exemple de code, de mon cru cette fois ci. C’est une implémentation d’un “mini” repeat que j’ai simplifié en supprimant les problématiques de parsing de l’expression notamment, mais le principe de la transclusion répétée y est employé.</p> <p>HTML&nbsp;:</p> <pre> 	&lt;body ng-app=&quot;MyApp&quot; ng-controller=&quot;MyController&quot;&gt; 		&lt;h1&gt;Hello Plunker!&lt;/h1&gt; 		&lt;ul my-repeat=&quot;list&quot;&gt; 			&lt;li&gt;&lt;strong&gt;{{element}}&lt;/strong&gt;&lt;/li&gt; 		&lt;/ul&gt; 	&lt;/body&gt; </pre> <p>JavaScript&nbsp;:</p> <pre> 	angular.module('MyApp', []) 		.controller('MyController', function($scope) { 			$scope.list = ['one', 'two', 'three']; 		}) 		.directive('myRepeat', function() { 			return { 				restrict: 'A', 				transclude: true, 				controller: function($scope, $element, $attrs, $transclude) { 					$scope.$watch($attrs.myRepeat, function(list) { 						$element.html(''); 						angular.forEach(list, function(element) { 						var childScope = $scope.$new(); 						childScope.element = element; 						$transclude(childScope, function(clone) { 							$element.append(clone); 						}); 					}); 				}); 			} 		}; 	}); </pre> <p><a href="http://plnkr.co/edit/VjOQ9I?p=preview">Le code fonctionnel peut être consulté sur Plunkr</a></p> <h4>Conclusion</h4> <p>En conclusion, je voulais aborder la question WebComponents. Comme tout le monde le dit, les WebComponents sont l’avenir du Web, et sont également l’avenir d’Angular car l’équipe de dév d’Angular a plusieurs fois affirmé que l’objectif d’Angular était de converger.</p> <p>Toutefois, si certains pensaient que les directives étaient exactement des WebComponents, j'espère que cet article leur a fait comprendre les différences de concepts.</p> <p>Ainsi, je finirais par cette question ouverte dont je n’ai pas la réponse, comment aborder Angular 2.0 avec les WebComponents pour toutes directives&nbsp;? C’est un de leurs défis pour la prochaine version majeure et je suis curieux de voir comment ils vont le relever.</p>