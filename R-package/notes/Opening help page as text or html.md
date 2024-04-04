
Could you run:

 file.path(R.home('etc'),'Rprofile.site')

This should return a path with the Rprofile file. Open the file in an editor and see which of the two options are commented out:

# set the default help type

# options(help_type="text")

  options(help_type="html")

For me text is commented out so everything is returned as html.

 On Windows, you get a choice during installation of R if oyu want to use text or html. Maybe your R version is set to text.

The idea is that the output should be defined to the user.

 help(bootGSEA, help_type = 'html')  
should get you to the HTML documentation; help(bootGSEA, help_type =  
'text') should give you plain text.

 The default depends on  
options(help_type=...)

Which depends on the Rprofile settings.

Maybe you shoudl try  help(bootGSEA, help_type = 'html') first and see if you get the html output and then you can try Rprofile