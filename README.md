# JSPatterns
Compilation of JS patterns
[Object Literal Pattern](https://codepen.io/anon/pen/OVZpqO?editors=1010)

```
//cdnjs.cloudflare.com/ajax/libs/jquery/2.1.3/jquery.min.js
https://cdnjs.cloudflare.com/ajax/libs/mustache.js/2.1.2/mustache.min.js

<div id="peopleModule">
    <h1>People</h1>
    <input placeholder="name" type="text">
    <button id="addPerson">Add Person</button>
    <ul id="people">
        <script id="people-template" type="text/template">
            {{#people}}
                <li>
                    <span>{{.}}</span>
                    <i class="del">X</i>
                </li>
            {{/people}}
        </script>
    </ul>
</div>
```

``` Javascripts
var people = {
    people: ['Will', 'Steve'],
    init: function() {
        this.cacheDom();
        this.bindEvents();
        this.render();
    },
    cacheDom: function() {
        this.$el = $('#peopleModule');
        this.$button = this.$el.find('button');
        this.$input = this.$el.find('input');
        this.$ul = this.$el.find('ul');
        this.template = this.$el.find('#people-template').html();
    },
    bindEvents: function() {
        this.$button.on('click', this.addPerson.bind(this));
        this.$ul.delegate('i.del', 'click', this.deletePerson.bind(this));
    },
    render: function() {
       var data = {
           people: this.people,
       };
       this.$ul.html(Mustache.render(this.template, data));
    },
    addPerson: function() {
        this.people.push(this.$input.val());
        this.render();
        this.$input.val('');
    },
    deletePerson: function(event) {
        var $remove = $(event.target).closest('li');
        var i = this.$ul.find('li').index($remove);

        this.people.splice(i, 1);
        this.render();
    }

};

people.init();
```

