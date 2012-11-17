Enaml
======
**Enaml is Not A Markup Language**

    A tool for building durable visual layers that hold up well
    under heavy use

|
|


Características
===============

- Inspirado en QML
- Pero usa widgets nativos
- como Glade pero mantenible!
- Lenguaje declarativo parecido a... Python!file:///home/tin/lab/enaml-talk/index.html#/
- ¡MVC fácil!


::

                      -> wxPython
    Enaml <-> Traits /
                     \
                      -> PyQt/PySide

- Made by Entought (conocen Scipy ?)

.. class:: hide-title

.
=

.enaml
------

.. class:: prettyprint lang-python

::

    from enaml.stdlib.fields import IntField

    enamldef PersonForm(Form):
        attr person
        Label:
            text = 'First Name'
        Field:
            value := person.first_name
        Label:
            text = 'Last Name'
        Field:
            value := person.last_name
        Label:
            text = 'Age'
        IntField:
            value := person.age


    enamldef PersonView(MainWindow):
        attr person
        PersonForm:
            person = parent.person

.py
---

.. class:: prettyprint lang-python

::

    from traits.api import HasTraits, Str, Range, on_trait_change

    class Person(HasTraits):
        """ A simple class representing a person object."""
        last_name = Str
        first_name = Str
        age = Range(low=0)

        @on_trait_change('age')
        def debug_print(self):
            """ Prints out a debug message whenever the person's age changes """
            templ = "{first} {last} is {age} years old."
            print templ.format(first=self.first_name,
                               last=self.last_name,
                               age=self.age)

    if __name__ == '__main__':
        import enaml
        with enaml.imports():
            from person_view import PersonView
        john = Person(first_name='John', last_name='Doe', age=42)
        view = PersonView(person=john)
        view.show()

Resultado
----------

.. image:: john_doe.png
   :align: center

Más
====

|
|

.. class:: center

    http://docs.enthought.com/enaml/
