# Login modal

## Native JavaScript for Bootstrap V4 Github

* [https://thednp.github.io/bootstrap.native/v5.html](https://thednp.github.io/bootstrap.native/v5.html)
* [https://thednp.github.io/bootstrap.native/v5.html\#componentModal](https://thednp.github.io/bootstrap.native/v5.html#componentModal)
* Ladda ned ramverket: [https://github.com/thednp/bootstrap.native/blob/master/dist/bootstrap-native-v5.min.js](https://github.com/thednp/bootstrap.native/blob/master/dist/bootstrap-native-v5.min.js)

### Modal

* Länka in Bootstrap CSS 
* Infoga modalrutans HTML-kod på sidan

```markup
<!-- blank modal template -->
<div id="modal" class="modal fade" tabindex="-1" role="dialog" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content"></div>
    </div>
</div>
```

### Skript.js

```javascript
const eLogin = document.querySelector("#login");

// initialize on a <div class="modal"> with all options
// Note: options object is optional
var myModal = new BSN.Modal(
    '#modal', // target selector
    { // options object
        content: '<div class="modal-body">Some content to be set on init</div>', // sets modal content
        backdrop: 'static', // we don't want to dismiss Modal when Modal or backdrop is the click event target
        keyboard: false // we don't want to dismiss Modal on pressing Esc key
    }
);

eLogin.addEventListener("click", function () {
    myModal.setContent('<div class="modal-header">' +
        '<h5 class="modal-title" id="myModalLabel">Modal title</h5>' +
        '<button type="button" class="close" data-bs-dismiss="modal" aria-label="Close">x</button>' +
        '</div>' +
        '<div class="modal-body">' +
        'Some content' +
        '</div>' +
        '<div class="modal-footer">' +
        '<button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>' +
        '<button type="button" class="btn btn-success">Save changes</button>' +
        '</div>');
    myModal.show();
});
```

## Formuläret

```markup
<form action="#" method="post">
    <label>Användarnamn <input type="text" name="anamn" required></label>
    <label>Lösenord <input type="password" name="losen" required></label>
    <button class="btn btn-primary">Logga in</button>
</form>
```

