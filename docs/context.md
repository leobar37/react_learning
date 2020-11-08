# context

provee una forma de pasar datos  a travéz del
árbol de componentes sin tener que pasar props manualmente
en cada nivel


## cuando usar context 

- Esta diseñado para datos que pueden considerarse globales 
  - como el usario autenticado actual
  - el tema 
  - el idioma

por ejemplo si tuvieramos que hacerle
saber a un boton que su tema es dark 
a continuacion pasamos un prop de tema 
para darle estilo a un componente button


```ts
class App extends React.Component {
  render() {
    return <Toolbar theme="dark" />;
  }
}

function Toolbar(props) {
  // El componente Toolbar debe tener un prop adicional "theme"
  // y pasarlo a ThemedButton. Esto puede llegar a ser trabajoso
  // si cada botón en la aplicación necesita saber el tema,
  // porque tendría que pasar a través de todos los componentes.
  return (
    <div>
      <ThemedButton theme={props.theme} />
    </div>
  );
}

class ThemedButton extends React.Component {
  render() {
    return <Button theme={this.props.theme} />;
  }
}

```
usando Context podemos evitar pasar
props a trávez de elementos intermedios 


## antes de usar context

Context se usa principalmente
cuando algunos datos tienen que ser
accesibles por muchos componentes en diferentes
niveles de anidamiento . 

> se debe aplicar con moderación por hacer que la reutilizacion 
de componentes sea más dificil 

 
## context provider 
cada Objeto Context  viene con un componente 
Provider de react que permite que los
componentes que lo consuman se suscriban  los
cambios del contexto.

`<MyContext.Provider value={/* algún valor */}>`

 
## context consumer

Un componente de React que se suscribe a cambios 
de contexto . Esto le permite suscribirse dentro
de un componente de  función
