*Start Part 10*

*this is the 10th part and the penultimate video in a video series dedicated to building a shopping cart application on net 6. so we are nearly finished building our shopping cart application in this video we are going to create functionality so that a user can filter the products in our stores product catalog by product category we will write codes to query our database for all the product categories within our database and display them as menu items in the main menu contained within the sidebar section of our ui when the user clicks one of the menu items denoting a product category data representing the products related to that category will be appropriately displayed to the user right let's get started so in the first part of this course we created our database through ef core code first migrations a requirement to update the databases seed data or structure may arise for example due to a decision to include new functionality within the application or perhaps just to correct a minor mistake made when the database was first created and seeded with data through ef core code first migrations we have the agility that we need to make appropriate adjustments to our database during the development and testing phases of our application so before we start writing code we need to address a database related requirement*

*we need to add a new column to the product categories database table where we can store relevant css code that denotes an icon used to represent a product category we are of course going to use ef core code first migrations to address this requirement so let's first update the product category entity class to include a new string property and let's appropriately name our new property icon css we are going to need an appropriate dto data transfer object to house the data that we send back to the client for when a client makes a request to the server for a collection of product category data so let's go to the shoponline.models project and create an appropriate class to represent the relevant dto let's go back to the shoponline.api project before we generate the relevant migration code let's open the shop online dbcontext class and update the relevant code for seeding our database within the onmodelcreating method
so here we are including relevant font awesome css classes within the new field named icon css these classes will be appropriately referenced within our code to render appropriate icon images for each of the relevant product categories so let's create our migration and give it a sensible name
great let's look at the migration code that we have just generated great let's run our migration through the update dash database command
excellent so let's go to our shoponline.api project so if we look at the product repository class we can see that we have already written the code for returning a collection of product category objects we need to expose this functionality to the relevant clients so to do this let's create an appropriate action method within the product controller class let's create an extension method to convert the collection of product category objects to a collection of
product category dto objects this may seem like a pointless exercise because the shape of the product category class is exactly the same as the shape of the product category dto class it is important to understand that even though this step may seem unnecessary that we are doing this due to design best practices why is this the design best practice in the future a new requirement may arise for example where a client may require additional data to be returned*

*from the relevant action method we want to maintain a clear separation of concerns between the dto classes and
the corresponding entity classes the reason for this is that the relevant
dto classes can evolve independently from the relevant entity classes if
required without affecting their counterpart entity classes
so a dto class can for example be extended without affecting its counterpart entity class
let's finish off the code for our action method
great so let's go to the shoponline.web project and write the calling client
code for retrieving a collection of product category data let's create the relevant service code
let's add an appropriate method definition to the i product service interface
let's implement the code for the interface that we have just created
so our code in this method is appropriately requesting a collection of objects of type product category dto
from the server great
let's create a razor component that will be responsible for outputting the product categories as menu items inside
our blazer applications main menu that resides within the sidebar section of our applications ui
so within the shared directory let's create a razor component named product categories nav menu
let's create a class named product categories nav menu base
let's write code so that an object of type i product service is injected into our razor component at
run time let's create a property of type i
enumerable that is strongly typed with the product category dto type
let's create a string property named error message
let's override the uninitialized async method
let's create code within the uninitialized async method that retrieves a collection of objects of
type product category dto from the server and assigns the returned collection to the product category dtos
property great let's implement the code for the product categories nav menu razer file
so we need to create a using directive that references the shoponline.web.pages
namespace so let's add the appropriate using directive to the underscore imports.razer file
we are adding this using directive because we are going to add appropriate tags
to the product categories nav menu razer file that reference relevant child razor
components that have been added to the pages directory
for example the display spinner child razor component
so notice that we are creating a link that contains a category id parameter
we'll later write code that uses this parameter value to query the server for a collection of product data that is
related to a particular category denoted by the relevant category id value
so we haven't yet written the code for the products by category raiser component
we'll write the code for this razor component a bit later this razor component will contain code
for displaying a collection of objects of type product dto that are related to the category id
value that will be passed as a parameter to the products by category razor component
so the next step is to reference our new razor component from within the razer
component that contains the main menu that appears to the user in the sidebar
of the ui so let's add the appropriate tag to reference our product categories nav
menu razor component
let's run the code
and we can see that our product categories are now appearing as menu items within the sidebar
however as you can see the style of the product category menu items are different from
the home menu item because the codes that produces the category menu item is contained within a
different razor component
so to solve this i'm simply going to copy the css code from the navmenu.razer.css file and paste it into
a new css file that we must name product categories nav menu dot razer dot css
so this will result in the product category menu items being styled like
the home menu item so we are flagrantly violating the
principle of `dry don't repeat yourself` here i'm doing this deliberately to keep up 
the momentum and creating the code for this application so that i can effectively keep the focus on the
aspects that are the subject of this part of the course you can of course centralize the css
code for the menu items in adherence with the principle of dry however for the reasons i've just explained i won't
address this issue in this part of the course
great so let's move on to create the code for filtering the products by category
let's go back to the shoponline.api project let's go to the i product repository
interface let's create a new method definition within the i product repository
interface the code that we'll implement for this method will be responsible for
retrieving a collection of product data that is related to a particular product category
so let's implement the code for the method that we have just defined within the product repository class
let's create an appropriate action method to expose this functionality to calling client code
great right let's go back to the shoponline.web project and implement the
service related code regarding the functionality for retrieving product data related to a particular category id
let's open the i product service interface and create an appropriate method definition
let's implement the code logic for the method definition that we have just created
so here we are appropriately requesting a collection of objects of type products dto
that are related to a particular product category
right let's create a razor component responsible for displaying the product data filtered by category on the ui
let's name this razor component products by category.razer
let's create a class named products by category base
let's implement the code for the products by category base class
firstly let's create a property that represents a parameter that will be passed into this razor component
the value passed into this category id parameter will be an appropriate
category id value note that we are able to declare that a property represents a parameter
by decorating the relevant property with the parameter attribute
let's create the other necessary properties for our razor component
so we want our collection of products to be retrieved for a particular category only when the category id parameter is
set so we can do this by implementing our code within a method that is called by
blazer in response to a life cycle event occurring when our parameter value is set
so to achieve this we are overriding a built-in blazer method named on parameters set async
so let's write the code within the on parameters set async method our code simply retrieves the
appropriate products data from the server based on the value passed into our category id parameter
let's write the appropriate ui code within the products by category.razer file
so let's first use the add page directive to appropriately declare the relevant root template information for
our products by category razer component
let's write code to inherit from the products by category base class
let's implement the code logic
so as you can see we can reuse our display products razor component
that we created in a previous part of this course to display the relevant products data to the user
let's run the code
excellent
so you can see that our product category menu items appear differently when compared to the home menu item
so let's fix this in code so that our menu items are displayed in a consistent
way to the user
great let's finish off by adding an appropriate logo for our application
excellent i hope you have enjoyed this video i look forward to presenting the final
video in this series where we'll optimize our code to potentially create better performance
for our application*

*End Part 10*
