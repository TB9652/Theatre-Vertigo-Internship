# Theatre-Vertigo-Internship
Code snippets and screen shots from project website

# Live Project

## Introduction
 For the last two weeks in the C# course at The Tech Academy, I worked with several other students developing a full-scale ASP.Net MVC and Entity Framework Web application.  
Using the Scrum/Agile project management methodology, I attended the sprint planning meeting , daily scrum meetings as well as the sprint retrospective.  Though the main part of the application was scaffolded using Entity Framework, there were ample opportunitiesDuring the two week
sprint, I worked on front-end and back-end stories of varying difficluties to include using code first migration to seed the database with test data and creating/modifying
one of the models and styling the pages.  The web application was for a local actor's theater in Portland called Theatre Vertigo.

  Below are descriptions of the stories I worked on, along with code snippets and navigation links. I also have some full code files in this repo for the larger functionalities
I implemented.

## Back End Stories
* [Seed Production Database](#seed-production-database)
## Front End Stories
* [Create Navbar](#create-navbar)
* [Create Modal Partial View](#create-modal-partial-view)

### Seed Production Database
 This database was seeded with test data using code first migration.  The test data consisted for fifteen rows and eleven columns of data meant to be representative of the type of data you would expect to see on a theatre company's website.  Even though DateTime would format both a date and a time for each property within the database, I only wanted for date to be dispalyed for the opening/closing date and only time for the Matinee and Evening showtimes when displayed on the web page so I added code to alter the display format.
 
                            using System;
                            using System.Collections.Generic;
                            using System.ComponentModel.DataAnnotations;
                            using System.Linq;
                            using System.Web;


                            namespace TheatreCMS2.Models
                            {
                                public class Production
                                {
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
                                }
                            }                
            

### Create Navbar

 Using the scaffolded NavBar as a template, I added the theater comapny's logo and made it a link back to the home page.  In the layout.cshtml file I moved the following code "@Styles.Render("~/Content/css")" so I could later over-ride the any bootstrap styling with my own CSS styling in the Site.css file then restructured the sacqffolded code so all navlinks were rendered in the same area of the navbar.  I added custom classes to apply CSS styling to the navbar.

 
         <!DOCTYPE html>
         <html>
         <head>
             <meta charset="utf-8" />
             <meta name="viewport" content="width=device-width, initial-scale=1.0">
             <title>@ViewBag.Title - My ASP.NET Application</title>
             @Scripts.Render("~/bundles/modernizr")
             @Styles.Render("~/Content/font-awesome.css")
             @Styles.Render("~/Content/font-awesome.min.css")
             @Styles.Render("~/Content/css")      @*This was moved down to allow for certain bootstrap styling to be over-ridden pertaining to the nav-links*@

             </head>
             <body>
               <nav class="navbar navbar-expand-lg navbar-light bg-light">
                   <div class="navbar-header">

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

                           </div>
                       </div>
                   </div>
               </nav>
               
### Create Modal Partial View
 
