FROM openanalytics/r-base

MAINTAINER Simon Garnier "garnier@njit.edu"

# system libraries of general use
RUN apt-get update && apt-get install -y \
    sudo \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev \
    libxt-dev \
    libssl-dev \
    libssh2-1-dev \
    libssl1.0.0

# system library dependency for the app
# RUN apt-get update && apt-get install -y \
#     libmpfr-dev

# basic shiny functionality
RUN R -e "install.packages(c('shiny', 'shinythemes', 'rmarkdown'), repos='https://cloud.r-project.org/')"

# install teachR package
RUN R -e "install.packages('devtools')"
RUN R -e "devtools::install_github('swarm-lab/teachR')"

# install dependencies of the opinion_dynamic app
RUN R -e "install.packages(c('ggplot2', 'dplyr', 'memoise', 'msm'), repos='https://cloud.r-project.org/')"

# copy the Rprofile to the image
COPY Rprofile.site /usr/lib/R/etc/

EXPOSE 3939

CMD ["R", "-e teachR::run_app('wisdom_of_crowds')"]
