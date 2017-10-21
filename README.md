# react-stateful-stateless-components
Este repositorio contiene el material explicado en el video tutorial de ReactJS v16 explicado en mi Canal de YouTube https://www.youtube.com/StevenPerezAlfaro

# ReactJS - Stateful Componet

```javascript
import React from 'react';
import PropTypes from 'prop-types';
import Titulo from './statelessFunctionalComponent';

/* d_ STATEFUL COMPONENT */

class StateFulComponent extends React.Component {
	constructor(props) {
		super(props);
		this.state = {
			nombre: 'John',
		};
	}

	componentWillMount() {
		// > Se ejecuta antes del render
		// > Evitar side effects en este evento
	}

	componentDidMount() {
		// > Se ejecuta luego del render
		// > Es el evento ideal para hacer peticiones http, actualizar el state (side effects).
		this.setState({ nombre: 'Steven' });
	}

	componentWillReceiveProps(nextProps) {
		// > Se ejecuta antes de que el componente (ya montado) se actualice con los nuevos props.
		(this.props.apellido !== nextProps.apellido) && this.setState({ apellido: nextProps.apellido });
	}

	shouldComponentUpdate() {
		// > Se ejecuta cuando cambia el state o algún prop
		// > No se ejecuta cuando se utiliza un this.forceUpdate();
		// > Cuando se retorna false, no se ejecutan los eventos:
		//    componentWillUpdate(), render() y componentDidUpdate()
		return true;
	}

	componentWillUpdate(nextProps, nextState) {
		// > Se ejecuta antes de que el componente (ya montado) haga el render con el
		//  state y props actualizados.
		// > No se debe ejecutar un this.setState({ ... }) ni acciones de Redux en este evento.
	}

	componentDidUpdate(prevProps, prevState) {
		// > Se ejecuta inmediatamente luego de que el render con las actualizaciones terminan.
		// > Se puede utilizar para hacer alguna interacción en el DOM.
	}

	componentWillUnmount() {
		// > Se ejecuta antes de que el componente se desmonte y se destruya.
		// > Se utiliza en casos para limpiar info del Redux Store, tiempos, elementos en DOM
		//    creados en el componentDidMount.
	}

	componentDidCatch(error, info) {
		// > Captura errores en el mismo componente y en los componentes hijos,
		//    pero no en el padre, abuelo.
		// > Se puede utilizar para mostrar un componente diferente de Error.
		console.log(error);
		console.log(info);
	}

	customEvent() {
		console.log('Custom');
	}

	render() {
		const customClass = this.state.nombre.length > 0 ? 'is-active' : '';
		this.customEvent();

		return (
			<div className={ `container ${customClass}` }>
				<h1 className="abc">Componente Padre</h1>
				<Titulo titulo="Componente Hijo"/>
			</div>
		);
	}
}

StateFulComponent.defaultProps = {
	apellido: 'Doe',
};

StateFulComponent.propTypes = {
	apellido: PropTypes.string.isRequired,
};

export default StateFulComponent;

```

# ReactJS - Stateless Componet

```javascript
import React from 'react';
import PropTypes from 'prop-types';

/* d_ STATELESS COMPONENT */

const Titulo = (props) => {
	return (
		<h1 className="container--title">{ props.titulo }</h1>
	);
};

Titulo.defaultProps = {
	titulo: 'Titulo Predefinido',
};

Titulo.propTypes = {
	titulo: PropTypes.string.isRequired,
};

export default Titulo;
```
