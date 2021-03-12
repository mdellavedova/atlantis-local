FROM runatlantis/atlantis:v0.15.1 as build

# Install terraform-compliance via a builder as it requires compilation binaries only during install
# See https://github.com/terraform-compliance/cli/issues/192#issuecomment-654309628
RUN apk add libxml2-dev libxslt-dev python3-dev gcc build-base
RUN python3 -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
RUN pip install terraform-compliance==1.3.12
RUN pip install pyyaml

# Install Terragrunt
RUN curl -L -o /usr/bin/terragrunt https://github.com/gruntwork-io/terragrunt/releases/download/v0.26.7/terragrunt_linux_amd64 && \
        chmod +x /usr/bin/terragrunt

# Get to Atlantis
FROM runatlantis/atlantis:v0.15.1 as release

RUN apk add python3

# Install Golang
RUN apk add --no-cache git make musl-dev go
ENV GOROOT /usr/lib/go
ENV GOPATH /go
ENV PATH /go/bin:$PATH
RUN mkdir -p ${GOPATH}/src ${GOPATH}/bin

# Install scenery
RUN git clone https://github.com/dmlittle/scenery
WORKDIR scenery
RUN go mod init github.com/dmlittle/scenery
RUN go mod tidy
RUN go get -u github.com/dmlittle/scenery


COPY --from=build /opt/venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

COPY --from=build /usr/bin/terragrunt /usr/bin/terragrunt
