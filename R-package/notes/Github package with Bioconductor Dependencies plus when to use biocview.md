
I asked the Bioconductor mailing list which deals with R package Development for Bioconductor.

They told me not to use the command you are using.

Instead you should use the following command:

BiocManager::install("klausjung-hannover/bootGSEA")

This works and installs all dependencies.

Your command will only install the package and requires the end-user to preinstall the depenencies before installing the package.

You can create a small file telling the user to use the BiocManager command, not the other one.

Also a small installation guide on the github package for the package could help. Right now the main package only should the licence agreement.

Otherwise you can submit your package to CRAN or Bioconductor.


------------------------


As was already mentioned, your easiest path forward is to first ask your users to install the
{BiocManager} package from CRAN, then use that to install your package.
As it is, you are already asking your end users to install {devtools} (really {remotes}) first in order
to install your package anyway, ie:
Instead of asking them to do this:

R> install.packages("remote")
R> remotes::install_github("klausjung-hannover/bootGSEA")


You should instead ask them to:

R> install.packages("BiocManager")
R> BiocManager::install("klausjung-hannover/bootGSEA")


While the remotes package still works, https://github.com/r-lib/pak is
now a better alternative. It also comes with built-in Bioconductor
support:
pak::pkg_install("klausjung-hannover/bootGSEA")
Thank you,
I am still wondering why everyone on the internet mentions adding "biocView" to the
DESCRIPTIOn-File. I couldn´t find a source for that but everyone on Biostart, Stackoverflow or
any other forum keeps mentioning adding biocView.
What does adding biocView do if anything? When should I add BiocView to the DESCRIPTION-
File?

Sorry if this is spam, I think my last message got bounced because my mail client converted the
GitHub link into a nice jpg.
As you mentioned, you can just add biocViews: Software to your
DESCRIPTION: https://github.com/r-lib/remotes/issues/477. If you need further explanation then
the code is
here: https://github.com/r-lib/remotes/blob/b9091cc471ea59471d10981330a868402e1b7bd9/install-
github.R#L687-L694
Adding the field causes remotes to add BioC to the repo list when installing dependencies. I think
it's worth doing so your users can use remotes if they want and not have to install/use other
installation managers.
Does it apply only to the remotes package or also to devtools::install_git function?
Sergej
I believe that devtools just uses remotes under the hood, so it should work.

BiocView is not for CRAN or Bioconductor packages, instead its for packages that need to be installed using remotes such as Github packages