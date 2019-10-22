# Das-Pagination

Pagination of lists in vue

## Project setup
```
npm install das-pagination
```

Add this to your data in your vue component
````
items: []
````
And this to your methods
````
getDataFromPagination (value) {
  this.items = value
}
````
Adding the component itself 
````
<pagination
:per-page="12"
:items="keysFiltered"
v-on:paginate="getDataFromPagination"/>
````
Where items is the list that needs to be paginated, per-page is the amount of items per page
and v-on:paginate is a function emitting the data back to the page.

Lastly go through this.items when looping through the items in the table
````
v-for="key in this.items"
````
