

`freezeTableName` si es true no intenta cambiar el modelo de esta tabla.

Se puede especificar para una tabla en especifico o para todas las tablas. En *define*.


Se puede configurar que los timestamps sean `false`. El tercer parámetro de *define*.

~~~

..,{
    timestamps:false
});

~~~

Tiene un monton de validaciones integradas. `ValidateMe` que te dice si es una url valida, un emai., una IPv4, isLowerCase, isCreditCard

~~~

...
name: {
    type: Sequelize.STRING,
    validate: {
        len:[3],
        contains: {
            args: ['foo'],
            msg: 'Error, field must contin foo'
        }
    }
}

~~~

---
## **Hooks**

Son llamados antes y después de los eventos que se producen cuando sequelize se ejecuta.

- `beforeValidate`
- `afterValidate`
- `beforeCreate`
- `afterCreate`

Se especifican en el tercer parametro del `define` del modelo.

Ejemplo:

~~~

let User = connection.define('User', {
    name: Sequelize.STRING,
    password: Sequelize.STRING
}, {
    hooks: {
        afterValidate: (user) {
            user.password = bcrypt.hashSync(user.password, 8);
        }
    }

});

~~~

generatedata.com

---
## **Create**

`.bulkCreate(_JSON)` -> para generar muchos datos.


---
## **Find**

~~~
User.findAll({
    where:{
        name: 'David',
        email: {
            [Op.like]: '%@gmail.com'
        }
    }
})

~~~


`findById(3)`


---
## **Update**

~~~
User.update({name:'joe', password:'123'},
    {
        where : {
            id:req.params.id
            }
    }).then(rows => {
        res.json(rows);
    }).catch(..)
});

~~~

---
## *Destroy*

~~~
User.destroy({where: {id:50}}).then(rows => {
        res.send('success deleted');
    }).catch(..);
~~~

---
## **Associations**

Relación entre distintas tablas **JOINs**.

`Post.belongsTo(User, {foreignKey:'userId'});`


El equivalente al fetch sería de esta manera:
~~~
Post.findAll({
    include: [
        model: User, as: 'UserRef'
    ]}
});
~~~

`Post.belongsTo(User, { as:'UserRef', foreignKey:'userId'});`

Tipos:
- OneToOne -> `User.hasOne(Post);` -> Solo uno.
- OneToMany -> `User.hasMany(Post);` -> Array de items.
- ManyToMany -> `User.belongsToMany(Post); Post.belongsToMany(User);` -> Join. Dos Arrays, uno por cada objeto.

~~~
User.findById('1', {
    include: Project, 'Tasks', attributes: ['name']
});

~~~


~~~
Proyect.create({
    name: 'project name'
}).then((proyect) => {
    project.setWorkers([1,2]);
    project.addWorkers(5);
});

~~~

---