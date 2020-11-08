## inicio
## Referencias y el dom


En flujo normal en datos de React,
las propiedades son la única forma 
en que los componentes padres pueden interactuar 
con sus hijos.Para renderizar un hijo vuelves
a renderizarlo con propiedades nuevas 

### cuando usar las referencias 

- Controlas enfoques, seleción de texto, o reproducción 
de medios
- activar animaciones imperativas
- integracion con bibliotecas DOM de terceros

### no abuses de las referencias 


## levantar el estado
significa que si dos componentes necesitan
ser sincronizados no usar refs hacer que su componente
padre maneje el estado de los dos y se convierta en la
fuente de verdad
[**ejemplo:**](./ejemplos/upstate.md)


### creando referecias

las referencias son creadas usar `createRef()` y
agregandolas a elementos de react mediante el 
atributo `ref`. Las referencias sonj asignadas
compumnete a una propiedad de instacia cuando 
un componente es construido , así pueden ser 
referenciadas por el componente

```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }
  render() {
    return <div ref={this.myRef} />;
  }
}
```
**accediendo a las referencias**

cuando una referencia es pasada a un elemento 
en el renderizado, una referencia al nodo pasa a ser accesible en el atributo current de la referencia

- > cuando el atriubuto `ref` es usado en un elemento
HTML, la referencia creada en el constructor con `Reac.createRef()` recibe el elemento DOM adyacente como su
propiedad `current`

- > Cuando el atributo ref es usado en un componente de clase personalizado, el objeto de la referencia recibe la instancia montada del componente como su atributo current.


[Example with input](./ejemplos/refs.md/#ejemplo-customTextInput)



**HOOK USE REF**
useRef devuelve un objeto ref mutable cuya propiedad .current se inicializa con el argumento pasado (initialValue). El objeto devuelto se mantendrá persistente durante la vida completa del componente.

Un caso de uso común es para acceder a un hijo imperativamente:

[function componen](./ejemplo/refs.md/#with-function)

## forwadRef

recibe como parametros la referencia y los 
props  se usa cuando se necesita 
cuando se quiere acceder a las propiedades
de un elemento creado con jsx




