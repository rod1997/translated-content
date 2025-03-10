---
title: IDBIndex.objectStore
slug: Web/API/IDBIndex/objectStore
translation_of: Web/API/IDBIndex/objectStore
---
{{ APIRef("IndexedDB") }}

La propriètè **`objectStore`** de l'interface {{domxref("IDBIndex")}} renvoie un accès au magasin d'objet que référence l'index.

{{AvailableInWorkers}}

## Syntaxe

```js
var indexObjectStore = myIndex.objectStore;
```

## Valeur

Un {{ domxref("IDBObjectStore","accès au magasin d'objet") }}.

## Example

Dans l'exemple suivant on ouvre une transaction puis un magasin d'objet et enfin l'index `lName`.

Le magasin d'objet référencé par l'index est afficher sur la console, quelque chose ressemblant à:

    IDBObjectStore { name: "contactsList", keyPath: "id", indexNames: DOMStringList[7], transaction: IDBTransaction, autoIncrement: false }

Finalement, On itère sur tous les enregistrements pour en insérer les données dans un tableau HTML. En utilisant la méthode {{domxref("IDBIndex.openCursor")}} qui travaille de la même façon que la méthode {{domxref("IDBObjectStore.openCursor")}} de l'{{domxref("IDBObjectStore","accès")}} au magasin d'objet sauf que les enregistrements sont renvoyés dans l'ordre de l'index et non celui du magasin d'objet.

```js
function displayDataByIndex() {
  tableEntry.innerHTML = '';

  //ouvre un transaction
  var transaction = db.transaction(['contactsList'], 'readonly');
  //accés au magasin d'objet
  var objectStore = transaction.objectStore('contactsList');

  //on récupère l'index
  var myIndex = objectStore.index('lName');
  //on affiche le magasin d'objet référencé locale sur la console
  console.log(myIndex.objectStore);

  //un curseur qui itère sur l'index
  myIndex.openCursor().onsuccess = function(event) {
    var cursor = event.target.result;
    if(cursor) {
      var tableRow = document.createElement('tr');
      tableRow.innerHTML =   '<td>' + cursor.value.id + '</td>'
                           + '<td>' + cursor.value.lName + '</td>'
                           + '<td>' + cursor.value.fName + '</td>'
                           + '<td>' + cursor.value.jTitle + '</td>'
                           + '<td>' + cursor.value.company + '</td>'
                           + '<td>' + cursor.value.eMail + '</td>'
                           + '<td>' + cursor.value.phone + '</td>'
                           + '<td>' + cursor.value.age + '</td>';
      tableEntry.appendChild(tableRow);

      cursor.continue();
    } else {
      console.log('Tous les enregistrements ont été affichés.');
    }
  };
};
```

> **Note :** Pour un exemple de travail complet, voir notre [To-do Notifications](https://github.com/mdn/to-do-notifications/) app ([view example live](http://mdn.github.io/to-do-notifications/)).

## Spécification

| Spécification                                                                                | Statut                       | Commentaire |
| -------------------------------------------------------------------------------------------- | ---------------------------- | ----------- |
| {{SpecName('IndexedDB', '#widl-IDBIndex-objectStore', 'objectStore')}} | {{Spec2('IndexedDB')}} |             |

## Compatibilité des navigateurs

{{Compat("api.IDBIndex.objectStore")}}

## Voir aussi

- {{domxref("IndexedDB_API.Using_IndexedDB","Utiliser IndexedDB")}}
- {{domxref("IDBDatabase","Débuter une connexion")}}
- {{domxref("IDBTransaction","Utilisé les transactions")}}
- {{domxref("IDBKeyRange","Définir l'intervalle des clés")}}
- {{domxref("IDBObjectStore","Accès aux magasins d'objets")}}
- {{domxref("IDBCursor","Utiliser les curseur")}}
- Exemple de référence: [To-do Notifications](https://github.com/mdn/to-do-notifications/tree/gh-pages) ([view example live](http://mdn.github.io/to-do-notifications/).)
