# `createCapsuleReference()`
The JavaScript function `createCapsuleReference()` will create a Danis³h Capsule Reference in the DOM.

______

## `createCapsuleReference()`

```js

let ashivaMenuNavigationObject = {
  capsuleName: 'Ash_Toggle_Input',
  publisher: 'Ash',
  classList: ['class1', 'class2'],
  StrongModifiers: {strong1: 'modStr1', strong2: 'modStr2'},
  attributes: {position: 'on', theme: 'dark'},
  Directives: {directive1: 'dir1', Directive2: 'dir2'},
  LightModifiers: {LightMod1: 'Light1', LightMod2: 'Light2'}
};

const createCapsuleReference = (capsuleReferenceObject) => {

  let StrongModifiers = (capsuleReferenceObject.hasOwnProperty('StrongModifiers')) ? capsuleReferenceObject.StrongModifiers : {};
  let classList = (capsuleReferenceObject.hasOwnProperty('classList')) ? capsuleReferenceObject.classList : [];
  let attributes = (capsuleReferenceObject.hasOwnProperty('attributes')) ? capsuleReferenceObject.attributes : {};
  let dataset =  (capsuleReferenceObject.hasOwnProperty('dataset')) ? capsuleReferenceObject.dataset : {};
  let Directives = (capsuleReferenceObject.hasOwnProperty('Directives')) ? capsuleReferenceObject.Directives : {};
  let LightModifiers = (capsuleReferenceObject.hasOwnProperty('LightModifiers')) ? capsuleReferenceObject.LightModifiers : {};

  let capsuleReference = '<';
  capsuleReference += capsuleReferenceObject.capsuleName;
  capsuleReference += ' (' + capsuleReferenceObject.publisher + ')';
  capsuleReference += (classList.length > 0) ? ' [+]class="' + classList.join(' ') + '"' : '';
  capsuleReference += (Array.isArray(StrongModifiers)) ? ' ' + Object.values(StrongModifiers).map((StrongModifier) => `${StrongModifier.charAt(0).toUpperCase() + StrongModifier.slice(1)}`).join(' ') : ' ' + Object.keys(StrongModifiers).map((StrongModifier) => `${StrongModifier.charAt(0).toUpperCase() + StrongModifier.slice(1)}="${StrongModifiers[StrongModifier].charAt(0).toUpperCase() + StrongModifiers[StrongModifier].slice(1)}"`).join(' ');
  capsuleReference += ' ' + Object.keys(attributes).map((attribute) => `[+]${attribute}="${attributes[attribute]}"`).join(' '); 
  capsuleReference += ' ' + Object.keys(dataset).map((datakey) => `[+]data-${datakey}="${dataset[datakey]}"`);
  capsuleReference += ' ' + Object.keys(Directives).map((Directive) => `[&]${Directive}="${Directives[Directive]}"`).join(' ');
  capsuleReference += (Array.isArray(LightModifiers)) ? ' ' + Object.values(LightModifiers).map((LightModifier) => `${LightModifier.charAt(0).toLowerCase() + LightModifier.slice(1)}`).join(' ') : ' ' + Object.keys(LightModifiers).map((LightModifier) => `${LightModifier.charAt(0).toLowerCase() + LightModifier.slice(1)}="${LightModifiers[LightModifier].charAt(0).toLowerCase() + LightModifiers[LightModifier].slice(1)}"`).join(' ');
  capsuleReference += '>';
  
  capsuleReference = capsuleReference.replace(/\s{2,}/g, ' ');

  return capsuleReference;
}

const ashivaMenuNavigationCapsuleReference = document.createComment('[' + createCapsuleReference(ashivaMenuNavigationObject) + ']');


// =================================
// =================================


// EXAMPLE OF createCapsuleReference
// ---------------------------------

let ashToggleInputObject = {
  capsuleName: 'Ash_Toggle_Input',
  publisher: 'Ash',
  LightModifiers: {'position': 'on'}
};

console.log('[<Ash_Toggle_Input (Ash) position="on">]'); // [<Ash_Toggle_Input (Ash) position="on">]
console.log('[' + createCapsuleReference(ashToggleInputObject) + ']'); // [<Ash_Toggle_Input (Ash) position="on">]


```


