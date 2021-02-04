# Theatre-Vertigo-Internship
Code snippets and screen shots from project website

# Live Project

## Introduction
 For the last two weeks in the C# course at The Tech Academy, I worked with several other students developing a full-scale ASP.Net MVC and Entity Framework Web application.  
Using the Scrum/Agile project management methodology, I attended the sprint planning meeting , daily scrum meetings as well as the sprint retrospective.  Though the main part of the application was scaffolded using Entity Framework, there were ample opportunitiesDuring the two week
sprint, I worked on front-end and back-end stories of varying difficluties to include using code first migration to seed the database with test data and creating/modifying
one of the models and styling the pages.  The web application was for a local actor's theater in Portland called Theatre Vertigo.

  Below are descriptions of the stories I worked on, along with code snippets, navigation links and screenshots. 

## Back End Stories
* [Seed Production Database](#seed-production-database)
* [Create Production entity Model](#create-production-entity-model)

## Front End Stories
* [Create Navbar](#create-navbar)
* [Create Modal Partial View](#create-modal-partial-view)
* [Create Production entity Model](#create-production-entity-model)
* [CRUD for Production](#CRUD-for-production)

### Seed Production Database
 This database was seeded with test data using code first migration.  The test data consisted for fifteen rows and eleven columns of data meant to be representative of the type of data you would expect to see on a theatre company's website.  Even though DateTime would format both a date and a time for each property within the database, I only wanted for date to be dispalyed for the opening/closing date and only time for the Matinee and Evening showtimes when displayed on the web page so I added code to alter the display format.
 
 ![Seed Productin Database](https://github.com/TB9652/Theatre-Vertigo-Internship/blob/main/Database%20seed.PNG)
 
                            
                                     context.Productions.AddOrUpdate(x => x.ProductionId,
                                     new Production() {
                                     ProductionId = 1,
                                     Title = "To Kill a Mockingbird",
                                     Playwright = "Aaron Sorkin",
                                     Description = "Harper Lee’s classic courtroom drama comes to thrilling life on stage.",
                                     OpeningDay = new DateTime(2021, 06, 07,  11, 00, 00),
                                     ClosingDay = new DateTime(2021, 06, 14, 19, 00, 00),
                                     Default = null,
                                     ShowtimeEve = new DateTime(2021, 06, 07, 19, 00, 00),
                                     ShowtimeMat = new DateTime(2021, 06, 07, 11, 00, 00),
                                     TicketLink = "",
                                     Season = 1,
                                     IsCurrent = false
                                     },
                              

### Create Navbar

 Using the scaffolded NavBar as a template, I added the theater comapny's logo and made it a link back to the home page.  In the layout.cshtml file I moved the following code "@Styles.Render("~/Content/css")" so I could later over-ride the any bootstrap styling with my own CSS styling in the Site.css file then restructured the sacqffolded code so all navlinks were rendered in the same area of the navbar.  I added custom classes to apply CSS styling to the navbar.
 
 ![Create Navbar](https://github.com/TB9652/Theatre-Vertigo-Internship/blob/main/NavBar.PNG)

 
         
             @Scripts.Render("~/bundles/modernizr")
             @Styles.Render("~/Content/font-awesome.css")
             @Styles.Render("~/Content/font-awesome.min.css")
             @Styles.Render("~/Content/css")      @*This was moved down to allow for certain bootstrap styling to be over-ridden pertaining to the nav-links*@

             
                       <a href="@Url.Action("Index", "Home")">
                           <img src="/Content/Images/cropped-TV_2transparent-1.png" />  @*This allows log to act as nav-link and acts as the Home button*@
                       </a>

                       <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
                           <div class="navbar-nav" id="navLink-align">
                               @*id added to over-ride bootstrap css and custom style nav-links*@

                               @*Custom class move-right added to over-ride bootstrap css and custom style nav-links*@
                               @*@Html.ActionLink("Home", "Home", "Home")*@  @*Commented out in case change is decided*@
                               @Html.ActionLink("About", "About", "Home", null, new { @class = "nav-item nav-link active move-right" })
                               @Html.ActionLink("Ensemble", "Ensemble", "Home", null, new { @class = "nav-item nav-link active move-right" })   @*Link for Ensemble view.  Needs                                 Ensemble view created*@
                               @Html.ActionLink("On Stage", "Index", "Production", null, new { @class = "nav-item nav-link active move-right" })   @* Link for OnStage view. *@

                               @Html.Partial("_LoginPartial")

### Create Modal Partial View
 I added a partial view to the shared folder in order to create a reusable Modal for the website so any Modals used would be consistant across the site.  The Modal was not being implemented, however I did test it to make sure it would display upon request.  I added temp photos for testing purposes.
 
 ![Create Modal Partial View](https://github.com/TB9652/Theatre-Vertigo-Internship/blob/main/Modal.PNG)

                              <!-- Button trigger modal -->
                              @*<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModalCenter">
                                Modal
                              </button>*@

                              <!-- Modal -->
                              <div class="modal fade" id="exampleModalCenter" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
                                <div class="modal-dialog modal-dialog-centered" role="document">
                                  <div class="modal-content">
                                    <div class="modal-header">
                                      <h5 class="modal-title" id="exampleModalLongTitle">Stupid Ghost, Savannah Reich</h5>
                                      <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                                        <span aria-hidden="true">&times;</span>
                                      </button>
                                    </div>
                                    <div class="modal-body">
                                      <img src="/Content/Images/Stupid_Ghost.jpg" />
                                    </div>
                                    <div class="modal-footer">
                                      <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                                      <button type="button" class="btn btn-primary">Save changes</button>
                                    </div>
                                  </div>
                                </div>
                              </div>

### Create Production entity Model

                              
                                      public int ProductionId { get; set; }
                                      public string Title { get; set; }
                                      public string Playwright { get; set; }
                                      public string Description { get; set; }
                                      [DataType(DataType.Date)]
                                      [DisplayFormat(DataFormatString = "{0:MM-dd-yyyy}", ApplyFormatInEditMode = true)]
                                      public DateTime OpeningDay { get; set; }
                                      [DataType(DataType.Date)]
                                      [DisplayFormat(DataFormatString = "{0:MM-dd-yyyy}", ApplyFormatInEditMode = true)]
                                      public DateTime ClosingDay { get; set; }
                                      public ProductionPhoto Default { get; set; }
                                      [DataType(DataType.Time)]
                                      [DisplayFormat(DataFormatString = "{0:hh:mm tt}", ApplyFormatInEditMode = true)]
                                      public DateTime ShowtimeEve { get; set; }
                                      [DataType(DataType.Time)]
                                      [DisplayFormat(DataFormatString = "{0:hh:mm tt}", ApplyFormatInEditMode = true)]
                                      public DateTime ShowtimeMat { get; set; }
                                      public string TicketLink { get; set; }
                                      public int Season { get; set; }
                                      public bool IsCurrent { get; set; }
                                

![Create Modal Partial View](https://github.com/TB9652/Theatre-Vertigo-Internship/blob/main/CRUD%20and%20styling.PNG)
