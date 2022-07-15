*start part 11*

*hi and welcome i'm gavin lon this is the 11th and final part in a
series of videos dedicated to building a shopping cart application using blazer
web assembly and web api on net six so we have now built our basic shopping
cart application but is software ever really 100 complete
at points there may be bug fixes to make we may need to upgrade our application
with the latest technologies a requirement may arise to improve the
overall performance of the application there may be parts of the application
where ux user experience can be enhanced in this video we are going to look
specifically at how we can improve the performance of our application by optimizing our code
there are two areas where we can potentially enhance the performance of our application item number one
in the web api component we are currently making two separate queries to the database when retrieving product
data our code is returning both product data and product category data to the calling
client to do this we are currently calling two separate methods in the product
repository class one for retrieving details about the products from the product database table
and the other for retrieving details about the product categories from the product categories database table
so in this video to potentially enhance performance we are going to retrieve the product and category details through one
query to the database instead of two the other area where we can improve
performance is by using local storage within the blazer component to store
both the product data and shopping cart data so that when our application needs
to retrieve relevant product data or shopping cart data our code can retrieve the relevant
information from local storage i.e data stored on the client within the user's
browser as opposed to making a trip as it were to the server every time the relevant data needs to be retrieved
so basically the travel time and retrieving the relevant data can be shortened in certain scenarios the data
can be retrieved on the client instead of the server
for content like this and much more please consider subscribing and please ring the bell so as to be notified of
future content if you like this video please hit the like button and please feel free to
share this video with anyone you feel may benefit from its content
so let's attack the first item let's go to the shoponline.api project
let's optimize the code on the server where we can make one query to the database to retrieve both product
information and related product category information rather than use two separate queries for this purpose
so the first step is that we need to modify the class representing the product entity
so we must first add a public property to the product class that is of type
product category
let's add the foreign key attribute to our new product category property we can
then pass an appropriate string value to the foreign key attribute that is used for declaring which
property in the product class must be used for joining the product entity to
the product category entity so this code will indicate to ef core as it were how
we want to join the product entity to the product category entity
let's go to the product repository class and first modify the get item method to
appropriately join the product entity to the product category entity in the relevant link query
so to do this we can use the include method like this we are establishing the join between the
two entities through this lambda expression notice the product category property
that we recently created within the product class for this query we only want to
retrieve one item so we can use the single or default async method to filter the product data
based on the relevant product id passed to this method
then for the get items method the code is similar to the get item method
but for the get items method we wish to return all the products that are currently stored in the products
database table with the related product category information to the calling code
so we of course don't need to filter the data so that means we don't need to use a
method like the single or default async method in this query
then the last method that we need to appropriately modify is the get items by category method
if we open the product controller class we can see that we can now simplify the code here but first we need to
appropriately update the relevant extension methods responsible for converting objects of type product to
objects of type product dto so let's first update the extension
method that converts an individual product to type product dto
great then let's update the conversion extension method that converts a collection of objects of type product to
a collection of objects of type product dto
great we can now update the relevant action methods accordingly
we no longer need to query for the category items in a separate query that we are using here to get a collection of
category items
so we've potentially improved performance of the server-side code through an appropriate code optimization
exercise we are only dealing with a small amount of data so the performance improvement
would probably be negligible but if we were dealing with large amounts of data the performance
improvement would be more significant so let's look at the second way that we
can improve the performance of our application the second way that we can improve the
performance of our application involves an update to our blazer component
so let's go to the shoponline.web project let's see how we can reduce the number
of trips to the server we are currently making for retrieving relevant product and shopping cart data
through the use of local storage so we could use javascript and blazer's
javascript interoperability feature and write our own local storage functionality
it turns out though we don't need to go to this kind of trouble because someone has already made available a new get
package that contains the local storage functionality we need so let's invoke the nuget package
manager window let's search for local storage
and this is the package we want to install so let's install the
blazered.localstorage nuget package
for more details regarding local storage please navigate to this url basically the javascript local storage
object allows you to save key value pairs in the browser
note the local storage object stores data with no expiration date the data is
not deleted when the browser is closed and are available for future sessions
so the local storage functionality provided to us within the blazid.localstorage nuget package
abstracts the javascript code for managing local storage so we don't need to write the relevant
javascript code ourselves we are now going to create two services
to encapsulate our local storage functionality so let's first create an interface named i manage products local
storage service
let's create two method definitions like this let's create an appropriate method definition for a method named get
collection
let's create an appropriate method definition for a method named remove collection
let's create an appropriate service class to implement the methods defined within the interface we have just
created
let's create a constructor whereby we indicate that we want an object of type i local storage service and an object of
type i product service injected into our constructor at run time
note that the i local storage service type is a type provided by the
blazer.localstorage nuget package that we have now installed so this type will be used to implement
the necessary local storage functionality
let's create a private method named ad collection
this method simply retrieves the product data from the server and saves the relevant product data in
the user's browser using local storage
okay let's create a string constant to store the key that will be used to identify the relevant value
in this case the relevant value is a serialized collection of objects of type product dto
let's implement the code for the get collection method so this method first tries to retrieve
the relevance data from local storage if the relevant data does not exist in
local storage we can call the add collection private method to retrieve the relevant data from the server and
save the relevant data to the user's browser using local storage the remove collection method simply
removes the relevant data stored within the user's browser using local storage
right let's create an interface within the contracts folder named i manage cart
items local storage service
let's create an appropriate method definition for a method named get collection
let's create an appropriate method definition for a method named save collection
let's create an appropriate method definition for a method named remove collection
right let's implement the relevant code for the interface that we have just created
so let's first create a class named manage cart items local storage service
let's create a constructor whereby we indicate that we want an object of type
i local storage service and an object of type i shopping cart service injected
into our constructor at runtime
let's create a constant to store the key that will be used to identify the
relevant items stored using local storage the local storage item in this
case will be a serialized collection of card item dto objects
let's create a private method named add collection
this method simply retrieves relevant data from the server and appropriately saves the data to local storage
this method attempts to retrieve the relevant data from local storage if the relevant data does not exist in local
storage the code retrieves the relevant data from the server and appropriately saves the relevant data to local storage
let's implement the code for the remove collection method which involves appropriately deleting a collection of
objects of type cart item dto from local storage notice that the key constant is used to
identify the relevant local storage item let's implement the code for the save
collection method which involves appropriately saving a collection of objects of type cart item dto to local
storage
so we haven't yet registered the ilocal storage service type provided in the
blazer.localstorage package with the dependency injection system so let's open our program.cs file
and apply the code to register the ilocalstorage service type for dependency injection
so we can use the add blazer local storage extension method for this purpose
we must then also register our two new service classes that we have created to
abstract the relevant local storage functionality with the dependency injection system
so let's now implement the relevant local storage functionality within the relevant razor components in order to
hopefully increase the performance of our blazer component let's open the products base class
this is the base class for the razor component that first loads when our application is first launched
let's create the code to ensure that our two local storage services are injected into this razor component
let's say that when the product's razor component is loaded we want to clear the relevant local storage items from local
storage this will force our code to retrieve the
relevant data from the server at this stage then subsequently we want the relevant
data retrieved from local storage to enhance performance
so let's create a private method named clear local storage and use the relevant functionality we have created within the
relevant services to remove the relevant data from local storage
let's call this method from within the uninitialized async method
then instead of going straight to the server for our data let's use the appropriate local storage service object
to first check to see if the relevant data resides within local storage
of course in this case we are clearing the data before this method is called which will force our code to retrieve
the data from the server however our code will subsequently save the data retrieved from the server to
local storage which means that when other razer components retrieve the relevant data
the data will be retrieved from local storage on the client side which means an unnecessary trip to the server will
be avoided so this gives us an idea of how we are able to increase performance of our
application using local storage we can also use our manage cart items
local storage service object to retrieve any cart item data that may be saved to the user's shopping cart
like this so in this case this code will retrieve
the relevant data from the server and save the data to local storage
any data retrieval of items within the user's shopping cart can then be done
from local storage and therefore trips to the server are saved and the performance of our application is
potentially enhanced let's appropriately update the shopping cart razor component
let's write the code so that an object of type i manage card items local storage service is injected into this
razor component at runtime
in the uninitialized async method let's replace the code that retrieves the relevant cart item data from the server
to get the relevant data from local storage
when a user updates the quantity of a particular item saved within the user's
shopping cart we must update the relevant local storage item this is because of course the relevant
shopping cart has now changed
we can appropriately implement the safe collection method for this purpose
we must also use the appropriate local storage service to implement the code to update the relevant local storage item
when a user removes an item from the user's shopping cart
let's implement the relevant local storage related code for the product details razer component
so this component is responsible for displaying details for a particular product
this razer component also contains functionality for adding a product to
the user's shopping cart
let's first create a private property to reference the shopping cart items collection here because when the user
adds a product to the user's shopping cart we want our code to update the relevant local storage item
we no longer only want the code to update the relevant shopping cart on the server we need to keep the client side
local storage data up to date as well so let's first write code to update our
shopping cart item's private property with data retrieved from local storage
within the uninitialized async method so within the method responsible for adding
a new item to the user's shopping cart we need to write code that not only
updates the data on the server but also updates the relevant local storage item
so we can implement the desired functionality in code like this
we can also now implement code that gets data for an individual product from local storage
great let's appropriately update the products by category razor component to include
local storage functionality
let's write code so that an object of type image products local storage service will be injected into this razor
component at runtime
let's write a private method so that the products filtered by category id are retrieved from local
storage
let's appropriately call our new private method from within the on parameters set
async method
lastly let's appropriately update the checkout razer component with our local
storage functionality
great let's run the code
excellent that definitely seems to have made a positive difference to the performance
of our shopping cart application if you've made it to the end of this
course well done you have learned quite a lot about laser web assembly and web api
we have also learned how to create a basic spy application where the vast majority of the code is implemented
using c-sharp i hope you have enjoyed going through this course as much as i enjoyed
creating it for content like this and much more please consider subscribing and please
ring the bell so as to be notified of future content if you liked this video please hit the
like button and please feel free to share this video with anyone you feel may benefit from its content
i really enjoy engaging with you in the comments section so please feel free to leave a comment
the latest code can be found on github a link to the relevant repository has been included below in the description
thank you and take care*

*End part 11*
