## Use a tag instead of "latest" for reproducibility
FROM rocker/binder:4.0.1

## Declares build arguments
ARG NB_USER
ARG NB_UID

## Copies your repo files into the Docker Container
USER root
## Enable this to copy files from the binder subdirectory
## to the home, overriding any existing files.
## Useful to create a setup on binder that is different from a
## clone of your repository
## COPY binder ${HOME}
RUN chown -R ${NB_USER} ${HOME}

## Run an install.R script, if it exists.
RUN R -e "remotes::install_github('geocompr/geocompkg')"

RUN wget https://github.com/robinlovelace/geocompr/archive/master.zip
RUN unzip master.zip
RUN mv geocompr-master /home/rstudio/geocompr
# COPY * /home/rstudio
RUN chown -Rv ${NB_USER} /home/rstudio

# Set RStudio preferences
# No inline code:
RUN echo '{' >> /etc/rstudio/rstudio-prefs.json
RUN echo '    "rmd_chunk_output_inline": false' >> /etc/rstudio/rstudio-prefs.json
RUN echo '}' >> /etc/rstudio/rstudio-prefs.json

## Become normal user again
USER ${NB_USER}

RUN if [ -f install.R ]; then R --quiet -f install.R; fi



