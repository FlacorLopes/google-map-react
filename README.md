
# Google Map React &middot; [![npm version](https://badge.fury.io/js/google-map-react.svg)](http://badge.fury.io/js/google-map-react) [![Build Status](https://travis-ci.org/google-map-react/google-map-react.svg?branch=master)](https://travis-ci.org/google-map-react/google-map-react) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](github.com/google-map-react/google-map-react/CONTRIBUTING.md)

`google-map-react` é um componente desenvolvido sobre  uma pequena parte do [Google Maps API](https://developers.google.com/maps/).
Ele permite a renderização de qualquer componente React no Mapa do Google. É totalmente isomórfico e consegue renderizar no servidor. Além disso, é capaz de renderizar componentes no navegador mesmo que o Google Maps API não esteja carregado. Internamente, ele usa um algoritmo de *hover* ajustável, permitindo interações de mouse em qualquer objeto no mapa. 

Ele te permite criar interfaces como essa do [exemplo](http://google-map-react.github.io/google-map-react/map/main) *(Você pode rolar a tabela, aplicar zoom e mover o mapa, passar o mouse sobre os marcadores e clicar neles, e clicar nas linhas da tabela)*
## Primeiros passoss

No caso mais simples, você só precisa adicionar as props `lat` e `lng` em qualquer componente.

[Veja funcionando no jsbin](https://jsbin.com/ruwogapuke/1/edit?js,output)

```javascript
import React, { Component } from 'react';
import GoogleMapReact from 'google-map-react';

const AnyReactComponent = ({ text }) => <div>{text}</div>;

class SimpleMap extends Component {
  static defaultProps = {
    center: {
      lat: 59.95,
      lng: 30.33
    },
    zoom: 11
  };

  render() {
    return (
      // Importante! Sempre defina a altura do container explicitamente
      <div style={{ height: '100vh', width: '100%' }}>
        <GoogleMapReact
          bootstrapURLKeys={{ key: /* SUA CHAVE DA API */ }}
          defaultCenter={this.props.center}
          defaultZoom={this.props.zoom}
        >
          <AnyReactComponent
            lat={59.955413}
            lng={30.337844}
            text="My Marker"
          />
        </GoogleMapReact>
      </div>
    );
  }
}

export default SimpleMap;
```

### Meu mapa não aparece!

- Certifique-se que o container contenha largura e altura. O mapa vai tentar preencher o componente pai, mas se o container não tiver tamanho definido, o mapa adquire largura/altura igual a  0. Isso não é um requisito do google-map-react, [mas sim um requisito do google-maps em si](https://developers.google.com/maps/documentation/javascript/tutorial).

## Instalação

npm:
```
npm install --save google-map-react
```

yarn:
```
yarn add google-map-react
```

## Recursos

### Funciona com seus próprios Componentes

Ao invés de usar os marcadores padrão, balões e outros componentes do Google Maps, você pode renderizar seus prórpios componentes react animados no mapa.

### Renderização isomórfica

Ele renderiza no servidor. *(Bem vindos, buscadores)* *Você pode desabilitar o javascript nas ferramentas do desenvolvedor do navegador, e recarregar qualquer página de exemplo para ver como funciona)*

### Posição dos componentes calculadas independente do Google Maps API

Ele renderiza os componentes no mapa antes de o Google Maps API estar carregado (até mesmo sem ele).

### Google Maps API Carrega sob demanda

Não é necessário inserir uma tag `<script src=` no topo da página. O Google Maps API é carregado a partir da primeira utilização do componente `GoogleMapReact`.

### Use a API do Google Maps 

Você pode acessar os objetos `map`e `maps`do Google Maps usando `onGoogleApiLoaded`. Nesse caso, é necessário definir a propriedade `yesIWantToUseGoogleMapApiInternals` para `true`.

```javascript
...

const handleApiLoaded = (map, maps) => {
  // usa os objetos map e maps
};

...

<GoogleMapReact
  bootstrapURLKeys={{ key: /* SUA CHAVE DA API */ }}
  defaultCenter={this.props.center}
  defaultZoom={this.props.zoom}
  yesIWantToUseGoogleMapApiInternals
  onGoogleApiLoaded={({ map, maps }) => handleApiLoaded(map, maps)}
>
  <AnyReactComponent
    lat={59.955413}
    lng={30.337844}
    text="Meu marcador"
  />
</GoogleMapReact>
```
OBS: Lembre-se de definir `yesIWantToUseGoogleMapApiInternals` como true.

[Exemplo](https://github.com/google-map-react/google-map-react-examples/blob/master/src/examples/Main.js#L69)
### Algoritmo de  *Hover* Interno

Agora é possível aplicar *hover* em todo objeto do mapa. (Contudo, você ainda pode usar seletores *hover* css se desejar) Se você der zoom no aqui nesse  [exemplo](http://google-map-react.github.io/google-map-react/map/main), ainda conseguirá passar o mouse sobre praticamente todos os marcadores do mapa.

## Exemplos

* Inserindo componentes react no mapa:
[simples](http://google-map-react.github.io/google-map-react/map/simple/) ([código](https://github.com/google-map-react/old-examples/blob/master/web/flux/components/examples/x_simple/simple_map_page.jsx))

* Opções do mapa personalizadas :
[exemplo](http://google-map-react.github.io/google-map-react/map/options/) ([código](https://github.com/google-map-react/old-examples/blob/master/web/flux/components/examples/x_options/options_map_page.jsx))

* Efeitos de *Hover*:
[hover simples](http://google-map-react.github.io/google-map-react/map/simple_hover/) ([código](https://github.com/google-map-react/old-examples/blob/master/web/flux/components/examples/x_simple_hover/simple_hover_map_page.jsx));
[distance hover](http://google-map-react.github.io/google-map-react/map/distance_hover/) ([código](https://github.com/google-map-react/old-examples/blob/master/web/flux/components/examples/x_distance_hover/distance_hover_map_page.jsx))

* Eventos do Google Maps:
[exemplo](http://google-map-react.github.io/google-map-react/map/events/) ([código](https://github.com/google-map-react/old-examples/blob/master/web/flux/components/examples/x_events/events_map_page.jsx))

* Projeto de exemplo:
[main](http://google-map-react.github.io/google-map-react/map/main/) ([código](https://github.com/google-map-react/old-examples/blob/master/web/flux/components/examples/x_main/main_map_block.jsx)); [balderdash](http://google-map-react.github.io/google-map-react/map/balderdash/) (mesmo código do principal)

* Agrupamento de marcadores (*clustering*) usando Hooks (**novo**: [código](https://github.com/leighhalliday/google-maps-clustering), [artigo](https://www.leighhalliday.com/google-maps-clustering)) [clustering-com-hooks](https://google-maps-clustering.netlify.com/)

* Exemplos de clustering ([código](https://github.com/istarkov/google-map-clustering-example))
[google-map-clustering-example](http://istarkov.github.io/google-map-clustering-example/)

* Como renderizar milhares de marcadores (**novo**: [código](https://github.com/istarkov/google-map-thousands-markers))
[google-map-thousands-markers](https://istarkov.github.io/google-map-thousands-markers/)

* Exemplos:
[Exemplos](https://github.com/google-map-react/google-map-react-examples)
[Exemplos antigos](https://github.com/google-map-react/old-examples)

* Exemplo no jsbin
[exemplo no jsbin](https://jsbin.com/ruwogapuke/1/edit?js,output)

* Exemplos no webpackbin (**novo**)
[documentação com os exemplos](./DOC.md) (Em construção)

* Exemplo no desenvolvimento local (novo)
[develop example](./develop)

## Documentação

Você encontra a documentação aqui:

- [Referência da API](./API.md)

- [Nova Documentação](./DOC.md) (Em construção)

## Contribua

O desenvolvimento local é dividido em duas partes (idealmente, usando duas abas)

Primeiro, execute npm start para observar a pasta `src/`e recompilar automaticamente a cada mudança.

```bash
npm start # runs rollup with watch flag
```
A segunda parte executará o `example/` criado por `create-react-app` que é linkado à versão local do seu módulo.

```bash
# (em outra aba do console)
cd example
npm start # runs create-react-app dev server
```

Agora, toda vez que você alterar algo no diretório  `src/` ou na pasta  `example/src` do app de exemplo, `create-react-app` irá  recarregar automaticamente seu servidor de desenvolvimento local e você pode iterar no seu componente em tempo real.

### link-install manual
Se você receber o erro`Module not found: Can't resolve 'google-react-map'...` ao executar o app de exemplo, você precisa linkar seu módulo de desenvolvimento local manualmente. Tente as opções a seguir:

  1. Na pasta raiz:
  ```bash
  npm link
  ```
  2. Navegue até `example/` e (após instalar outras dependências) execute:
  ```bash
  npm link google-map-react
  ```

## Licença

[MIT](./LICENSE.md)

## Problemas conhecidos

* Navegadores antigos precisarão de um polyfill pra suportar as Promises do ES6 para funcionar.

## !!! Buscamos colaboradores
Estamos constantemente buscando colaboradores. Por favor, envie uma mensagem ao prorietário ou qualquer outro colaborador.
