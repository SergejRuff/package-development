
Regarding your question from todays prasentation.

I just checked with the R dev mailing list on how to handle Bioconductor dependencies which are not suggested but Imported or Depends.

First. If your package is under the Suggests Field, the things I said in the prasentation still apply.

Note that someone wanting to run the examples/tests/vignettes may not have a suggested package available (and it may not even be possible to install it for that platform). The recommendation used to be to make their use conditional _via_ if(require("_pkgname_")): this is OK if that conditioning is done in examples/tests/vignettes, although using if(requireNamespace("_pkgname_")) is preferred, if possible.

However, using require for conditioning _in package code_ is not good practice as it alters the search path for the rest of the session and relies on functions in that package not being masked by other require or library calls. It is better practice to use code like

   if (requireNamespace("rgl", quietly = TRUE)) {

      rgl::plot3d(...)

   } else {

      ## do something else not involving rgl.

   }

You can read more about it in [https://cran.r-project.org/doc/manuals/R-exts.html#Suggested-packages](https://cran.r-project.org/doc/manuals/R-exts.html#Suggested-packages) under 1.1.3.1

Regarding Bioconductor Dependencies in Imports and Depends, i got the following opinion from one of the members of the mailing list

> Also for the future - how Do i provide Bioconductor dependencies as "Imports" for a package that I want to submit to CRAN?  
  
Just list it as you would a CRAN package.  The CRAN docs talk about  
"mainstream repositories"; I forget what the definition is of that  
(maybe repositories listed in `file.path(R.home(),  
"etc/repositories")`?), but definitely BioConductor is included.  
  
> Do I need to make that also conditional? I know I should provide Installation description in a readme fiel but how do I make sure  
  
No, you don't need to check.  If any imported package is not available,  
your package will not load, so errors will happen before you ever get to  
running examples.  
  
> that the Bioconductor dependencies dont cause a rejection from CRAN?  
  
Just make sure they exist on BioC and your code works with them.  
  
Duncan Murdoch

If that is correct, then I made a small mistake when answering your question.

It´s still good practice to make sure your code fails gracefully when the package is missing.

For that you can take a look at the Seurat package.

Under Utils.R (line 349-379) of the SeuratObject-Package ([https://cran.r-project.org/src/contrib/Archive/SeuratObject/](https://cran.r-project.org/src/contrib/Archive/SeuratObject/)) you will find the PackageCheck-function

which used by the Seurat-Package ([https://cran.r-project.org/src/contrib/Archive/Seurat/](https://cran.r-project.org/src/contrib/Archive/Seurat/)) to check if packages are alredy installed.

  
You can find examples for DEseq2 under differential_expression.R (starting line 1314 or you cntr+f for packagecheck) in the Seurat.package ([https://cran.r-project.org/src/contrib/Archive/Seurat/](https://cran.r-project.org/src/contrib/Archive/Seurat/))

or for limma (starting line 2292).

You can try with or without a conditional function for Imports-dependencies.

If I get any more Information regarding that topic I will let you know.

--------

i have another answer from the r dev mailing list.

  

> Thanks,  
>  
>  
> So is it just necessary for suggested packages.  
  
Those and "Enhances" packages, but hardly anyone uses "Enhances".  
>  
>  
> So, is it just good practice to make a conditional check?  
  
No, it is a requirement if the package is used but is not listed in  
Depends or Imports.  
  
If the package is in Depends or Imports it is a waste of time to make  
the check:  it will always succeed.  
  
Duncan Murdoch  

  

second opinion

  

CRAN is fine with Bioconductor Depends: and Imports: dependencies, as previously mentioned. This is because the CRAN maintainers explicitly configure their system to know about Bioconductor package repositories.

Users face a different challenge -- many users will not have identified (e.g., via `setRepositories()` a Bioconductor repository, so when they try to install your package it will fail in a way that you have no control over -- a generic message saying that the Bioconductor dependencies was not found.

You could mitigate this by advertising that your CRAN package should be installed via `BiocManager::install("<your CRAN package>")`, which defines appropriate repositories for both CRAN and Bioconductor, but there is no way to unambiguously communicate this to users.

Martin

  

I just checked Seurat again and saw that DEseq is in Suggests, not Imports. It was in imports in an earlier version.

Meaning it would require a conditional function anyway.

  

  

You can still implement a conditional function to ask the end-user if they want to install your dependency if Bioconductor is not a repository under SetRepositories().

Here you can use my example from the prasentation.

But you dont need a conditional function for the CRAN test according to the mailing list if the Depency is not part of suggests.

Suggested packages need a conditional fnction.

  

The people are trustworthy.

Martin Morgan runs the Bioconductor project and is part of the core team ([https://www.bioconductor.org/about/core-team/](https://www.bioconductor.org/about/core-team/))

Murdoch is the mentainer of rgl and other packages already available on CRAN

  

I hope that answers your question.