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
* [Create Navbar for Shared Layout.cshtml](#create-navbar-for-shared-layout.cshtml)

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
            

## Create Navbar for Shared Layout.cshtml
