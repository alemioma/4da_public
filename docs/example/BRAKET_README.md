# Braket Design Pattern

## Overview
In our documentation's examples, we utilize a JavaScript design pattern called Braket, designed specifically for frontend engineering. This pattern is built on standard HTML5, allowing developers the flexibility to incorporate more advanced techniques, such as web components, although they are not mandatory for successful project implementation.

## Components of Braket

### Bra
The `Bra` component is responsible for network communication. It listens to events and sends requests. Developers can implement this using `socket.io` or a combination of Server-Sent Events (SSE) and HTTP requests.

`Bra` includes two method types:
- `sendXXX`: Sends data to the network, targeting the topic `XXX`.
- `onXXX`: Handles incoming data from the network associated with the topic `XXX`.

### Ket
The `Ket` component manages user interaction and UI updates. It mirrors the method structure of `Bra`, with `sendXXX` methods being replaced by `updateXXX`.

### Glue
The `glue` module acts as an intermediary between `Bra` and `Ket`, handling data transformation and delivery. It consists of two main function classes:
- Klue. Functions that transform data from `Ket` and deliver it to `Bra`. These functions format or aggregate UI data for network transmission.
- Blue. Functions that transform data from `Bra` and deliver it to `Ket`. They parse or enrich network data for UI updates.


### Braket
The `Braket` class integrates `Bra` and `Ket`, facilitating full-stack application development. The implementation typically resides in a module named `braket.js`.

#### Example: braket.js
```javascript
import Bra from './bra.js';
import Ket from './ket.js';
import {Klue, Blue} from './glue.js';

let klue = new Klue();
let blue = new Blue();

let bra = new class extends Bra {
    constructor() {
        super();
    }

    onHello(data) {
        ket.updateHello( blue.decrypt(data) );
    }
};

let ket = new class extends Ket {
    constructor() {
        super();
    }

    onHello(data) {
        bra.sendHello( klue.encrypt(data) );
    }
};


#### Example: bra.js
```javascript

export default class Bra {
    constructor() {
        this.socket = io();

        this.socket.on('hello', data => this.onHello(data));
    }

    onHello(_) {}

    sendHello(_) {}
}


#### Example: ket.js
```javascript

export default class Ket {
    constructor() {
        // Assuming there's a button with id 'send'. When pressed, a message is sent.
        document.getElementById('send').onclick = () => this.onHello('hello at ' + Date.now());
    }

    onHello(_) {}

    updateHello(data) {
        // Assuming there's a label with id 'message'.
        document.getElementById('message').innerText = data;
    }
}


### Example: glue.js
```javascript

export class Klue{
	constructor(){
	}

	encrypt(data){
		return '*' + data
	}
}

export class Blue{
	constructor(){
	}

	decrypt(data){
		return data.slice(1)
	}
}
