Dockerfile
- https://docs.docker.com/engine/reference/builder/
- docker build -t shykes/myapp -f /path/to/a/Dockerfile .
- The ${variable_name} syntax also supports a few of the standard bash modifiers as specified below:
  ${variable:-word} indicates that if variable is set then the result will be that value. If variable is not set then word will be the result.
  ${variable:+word} indicates that if variable is set then word will be the result, otherwise the result is the empty string.
- .dockerignore # * any(except/)  ** any  ! not  

# FROM
- create basis image
  https://docs.docker.com/engine/userguide/eng-image/baseimages/#create-a-full-image-using-tar
  https://github.com/moby/moby/blob/master/contrib/mkimage-yum.sh
 
- FROM <image>[@<digest>|:<tag>] [AS <name>]  # d~ image:latest
- FROM scratch # Docker’s reserved, minimal image

# LABEL
- self.property
- LABEL k=v

# ENV
- to update environment variable(ig: PATH, VERSION)
- Command line arguments to docker run <image> will be appended after all elements in an exec form ENTRYPOINT, and will override all elements specified using CMD ==> exec form
- The shell form prevents any CMD or run command line arguments from being used, but has the disadvantage that your ENTRYPOINT will be started as a subcommand of /bin/sh -c, which does not pass signals. ==> shell form 
- you can override the ENTRYPOINT setting using --entrypoint, but this can only set the binary to exec (no sh -c will be used).

# ARG
- docker build command using the --build-arg <varname>=<value> flag
- ARG <name>[=<default value>]
- An ARG variable definition comes into effect from the line on which it is defined in the Dockerfile not from the argument’s use on the command-line or elsewhere
- ENV instruction always override an ARG instruction of the same name
- use ARG variable which changed will cause cache missed

# Predefined ARGs
- HTTP_PROXY
- http_proxy
- HTTPS_PROXY
- https_proxy
- FTP_PROXY
- ftp_proxy
- NO_PROXY
- no_proxy

# SHELL 
- SHELL ["executable", "parameters"]
- override default shell used for the shell form 

# RUN
- for run command
- RUN <command> (shell form, the command is run in a shell, which by default is /bin/sh -c on Linux or cmd /S /C on Windows)
- RUN ["executable", "param1", "param2"] (exec form)
- RUN apt-get update && apt-get install -y # RUN apt-get update in one line will treat as cached compared to the last Dockerfile change
- RUN set -o pipefail && wget -O - https://some.site | wc -l > /number # mark, set -o pipefail
- RUN ["/bin/bash", "-c", "set -o pipefail && wget -O - https://some.site | wc -l > /number"] # specific shell, and "-c"  shell processing else does not invoke a command shell(no shell profile will excuted)
- The exec form is parsed as a JSON array, which means that you must use double-quotes (“) around words not single-quotes (‘).

# CMD
- for executing container's defaults running executor command, only last one will take effect
- CMD ["executable","param1","param2"] (exec form, this is the preferred form)
- CMD ["param1","param2"] (as default parameters to ENTRYPOINT)
- CMD command param1 param2 (shell form)

# ENTRYPOINT
- set the image’s main command

# EXPOSE
- the ports on which a container will listen for connections

# ADD or COPY
- COPY is preferred, for size matters, wget|curl&&delte instand of this directive
- COPY only supports the basic copying of local files into the container
- ADD has some features (like local-only tar extraction and remote URL support) that are not immediately obvious
- If you have multiple Dockerfile steps that use different files from your context, COPY them individually, cache is more persistent  
# VOLUME
- expose any data storage area

# USER
- USER <user>[:<group>] or USER <UID>[:<GID>]
- like RUN groupadd -r postgres && useradd --no-log-init -r -g postgres postgres

# WORKDIR
- WORKDIR /path/to/workdir

# ONBUILD
- ONBUILD directive xx # add triger to exec in next Dockerfile build(From)

# STOPSIGNAL
- STOPSIGNAL [SIGKILL] 
- the signal sent when stop

# HEALTHCHECK
- tells Docker how to test a container to check that it is still working.

# 
