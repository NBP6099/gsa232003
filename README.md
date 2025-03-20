# gsa232003
//// models    restaurants.js
 promoted: {
 allowNull: false, //no puede ser nulo, viceversa true
 type: DataTypes.BOOLEAN,
 defaultValue: false //opcional si especifica como debe empeza
 }

//// migrations    create-restaurant.js

igual pero sequelize

//// restaurant controller.js
index y index owner para cambia order 
 order: [['promoted', 'DESC'], [[{ model: RestaurantCategory, as: 'restaurantCategory' }, 'name', 'ASC']]] 

 order: [['promoted', 'DESC']] 

CREAR FUNCION
const toogleRestaurant = async function (req, res) {
  try {
  // TODO toggle Pinned Restaurant
    const restaurantToBeToggled = await Restaurant.findByPk(req.params.restaurantId)
    if (restaurantToBeToggled.pinnedAt) {
      restaurantToBeToggled.pinnedAt = null
    } else {
      restaurantToBeToggled.pinnedAt = new Date()
    }
    await restaurantToBeToggled.save()
    res.json(restaurantToBeToggled)
  } catch (err) {
    res.status(500).send(err)
  }
+añadirla debajo la nueva
//// restaurantvalidation.js

 check('promoted').optional().isBoolean().custom(checkRestaurantPromoted), 
o 
  check('pinned').optional({ nullable: true, checkFalsy: true }).isBoolean(), // implementado nuevo

//// restaurant.routes.js
  app.route('/restaurants/:restaurantId/togglePinned') // IMPLEMENTADO
    .patch(
      isLoggedIn,
      hasRole('owner'),
      checkEntityExists(Restaurant, 'restaurantId'),
      RestaurantMiddleware.checkRestaurantOwnership,
      RestaurantController.toogleRestaurant)
funcion creada en restaurantcontroller
