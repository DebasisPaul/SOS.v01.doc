*2:06:12
This is the fifth part in a video series dedicated to building a shopping cart application using blazor web assembly on .net 6. so we have completed the implementation of two workflows `the first workflow involves retrieving the data pertaining to the products sold by our online store and `displaying the data in an aesthetically pleasing style to the user` `the second workflow involves displaying details for a particular product to the screen in response to the user clicking on a card representing the relevant product`. In this video we'll create the functionality whereby the user clicks the add to cart button which is available on the screen where details for a particular product are displayed this button click action will result in the relevant product being added to the
user's shopping cart after the user has clicked the add to cart button the user will subsequently be navigated to a screen that displays data pertaining to the products currently contained within the user's shopping cart*

*2:07:27
so let's get started so let's first implement the functionality for the server side code. so let's go to our project that contains the functionality for our web api component. in the second part of this video series we implemented the repository design pattern for functionality to handle database interactions regarding the products sold by our online store. so we now want to create the code for handling the database functionality pertaining to the shopping cart so let's create an interface that contains the method definitions for the shopping cart repository class that we'll create once we have created its interface so let's create an interface named i shopping cart repository let's create a method definition for a method named add item as the name suggests the code that we'll implement for this method will add a particular product to the relevant user's shopping cart let's add a method definition for a method named update qty when a user first adds a product to the user's shopping cart*

*2:09:07
the quantity of the relevant product added to the user's shopping cart will be won by default the implementation for this method will involve updating the quantity of a particular product that is currently contained within a user's shopping cart let's add a method definition for a method named delete item as the name suggests the functionality for this method will involve removing a particular product from the user's shopping cart the get item method will contain functionality for retrieving data regarding a particular product that is currently in the user's shopping cart the get items method will contain functionality for retrieving data for all the products that are currently in a particular user's shopping cart so let's create a class named shopping cart repository 
let's write codes to implement the i shopping cart repository interface that we have just created let's position our mouse pointers appropriately and press control period in order to bring in the appropriate namespace ie where the i shopping cart repository interface resides*

*2:10:43
let's press control period and generate the code staffs for the method definitions that we included within the i shopping cart repository interface so in this video we are going to implement functionality for three of the methods that we have defined within the i shopping cart repository interface namely add item get items and get item before we do this let's create a constructor let's add a parameter to our constructor that is of type shop online db context by including this parameter we are indicating to .net that we want an object of this type injected into our shopping cart repository class at runtime we have already registered the shop online db context type for dependency injection the shop online db context type is the ef core database context object that is used for handling data manipulation and data retrieval functionality in relation to our applications database*

*2:12:04
so let's implement the functionality for the add item method let's first write a link query that ensures that the product that the user is attempting to add to the user's shopping cart exists in the products table so if the item returned from our link query is not null we want code to execute that adds the relevant product to the cart items database table this denotes that the product has been added to the user's shopping cart so let's implement the code to add the item to the cart items database table once we have called the add async method we must also remember to call the save changes async method then we can write code to return the entity that has been successfully added to the cart items database table like this if an item is not successfully added to the database we want code to execute that will return null to the calling code so in order to avoid a product being added twice to our user's shopping cart 
let's implement code that checks to see if the relevant product already exists*

*2:13:36
within the user's shopping cart let's implement the code for this in a private method that returns a boolean value then we can use the private method we have just created like this to perform the relevant check so we have ensured that only one instance of a particular product can be added to the user's shopping cart please note that the user will be able to purchase more than one instance of a particular product by appropriately modifying the qty or quantity field we'll implement this at a later stage let's implement the code for the get items method let's write code that returns the results of a link query pertaining to the products currently stored within the user's shopping cart then let's write code for the get item method let's write code that returns the results of a link query which is data pertaining to a particular product currently stored within the relevant user's shopping cart let's add a controller class to the controllers folder let's name this controller class shopping cart controller*

*2:17:35
firstly let's create a constructor that contains two parameters one of type ishopping cart repository and the other of type i product repository let's create two read-only fields to reference the objects that will be injected into our controller class at runtime let's of course not forget to register the i shopping cart repository type for dependency injection so let's implement the code for the get items action method let's use our shopping cart repository object to return the items currently stored within the relevant user's shopping cart if no items are contained within the shopping cart we want code to execute that returns a http response of no content to the calling client this is denoted by a http code status of*

*2:19:30
204 so this means the client http request was successful but no items related to the client's request are present in the system therefore no content can be returned to the calling client so we are returning a collection of type cartt item dto to the client from the action method we have just written code that retrieves a collection of objects of type cart item we want to return a collection of objects of type cart item dto to the calling client the cart item dto type contains additional data regarding the relevant product we don't have the additional data at this point so let's use the product repository object to retrieve a collection of objects of type product we can then write code to join our collection of cart item objects with the collection of objects of type product using a link query and return an appropriate collection of objects of type can't item dto*

*2:20:35
to the calling client so let's keep this code clean and implement a linq query in an extension method to return the relevant collection of objects of type cart item dto to the get items action method before we do this let's write code to throw an exception if no products exist within the system because if there are no products in the system and the user is attempting to add a product to the user's shopping cart well this won't make any sense so this means an exception has occurred let's write code in a catch block that returns a http status code of 500 to the calling code so if for some reason an exception occurs during the execution of the get items action method we want an internal server error 500 http response to be returned to the client so let's go to the dto conversions class and implement another extension method overload named convert to dto.*

*2:21:39
we'll be able to call this extension method overload on an i enumerable collection of type cart item to perform the relevant conversion functionality let's go to our get items action method and call the extension method we have just created to return the appropriate collection of objects of type cart item dto we can then write code to return this collection to the calling client with a http response status code of 200 okay let's implement the code for the get item action method you can see here that the code is very similar to the get items action method but we of course are only returning one item of type cart item dto to the calling client instead of a collection of objects of type cart item dto so let's write code for converting an object of type cart item to an object of type cart item dto to do this let's go to the dto conversion class and implement the code for the appropriate extension method overload we can then call the relevant convert to dto extension method on the relevant object of type cart item to perform the appropriate conversion functionality*

*2:26:14
let's write the functionality for handling a post request from the client whereby a user is attempting to add a product to the user's shopping cart so let's write code to call the add item method on the shopping cart repository object that will be injected into our controller class at runtime we want to return the newly added item of type cart item dto to the calling client so we can call the same conversion code that we implemented for the get item method for this purpose it is important to note that it is standard practice for a post action method to return the location of the resource where the newly added item can be found this location will be returned in the header of the http response returned from this method we can use the create at action method to ensure that we are adhering to this*

*2:27:53
standard practice so the relevant resource can be found at the uri universal resource identifier pertaining to the get item action method and we are including the id of the newly added resource here and for the final argument we are including the newly added object which we have now converted to type cart item dto if you'd like to read more about the create at action method i've included an appropriate link below in the description and we of course need to decorate this action method with the http post attribute let's run the shoponline.api project through visual studio and you can see the new action methods and relevant dtos are present on the swagger ui web page great let's implement the relevant code for our blazer component so let's go to the shoponline.web project let's create a new service class where we'll implement code that interacts with the action methods that we have created within our shopping cart controller class in our web api project firstly let's create the appropriate interface in the contracts folder for the relevant service class let's name this interface i shopping cart service. let's create a method definition for the get items method and the add items method*

*2:31:06
let's create a class named shopping cart service let's generate the code staffss for the methods defined within the i shopping cart service interface 
let's create a constructor for the shopping cart service class let's include a parameter of type http client as a parameter within our constructor this parameter indicates to .net that we want an object of type http client injected into this class at runtime let's implement the code for the add item method 
so basically this code calls the post action method that we implemented in the shopping cart controller class if the response http status code is within the success range let's check to see if any content was returned if no content was returned let's return the default c-sharp value for the cart item dto type to the calling code which will be null if content was returned from the server let's return the object representing the newly created shopping cart item to the calling code this will of course be an object of type cart item dto let's include the relevant exception handling code let's implement code for the get items method so i'm deliberately including an incorrect uri universal resource identifier reference here so that this will force an exception when we run the code we'll fix this*

*2:34:21
a little bit later after we have run the code that tests how an application handles the relevant exception this code simply places a http get request to the get items action method and if content is returned returns the relevant content to the relevant razer component i.e the calling code let's go to the product details base class and implement a button click event handler method for the add to cart button let's name this click event handler method add to cart underscore click let's make sure that we have registered the i shopping cart service type for dependency injection let's implement code that ensures that an object of type i shopping cart service is injected into the product details base class at runtime then our code within the add to cart underscore click event handler method calls the add item method on the injected shopping cart service object to add a product chosen by the user to the user's shopping cart*

*2:37:55
let's go to the product details.razer file and implement the code that calls the add to cart underscore click event handler method so we have started with the implementation of the shopping cart functionality we have not implemented user registration or login functionality ie membership functionality in this application we could implement codes to bring down user related information from the server when the user first logs onto the system the information could include the user's user id and the user's cart id so because we haven't implemented login functionality let's temporarily hard code the user's cart id and user id in a class within the project that contains our blazer functionality so that we can progress with the implementation of the shopping cart functionality so in the first video in this series we seeded the data with data for two users*