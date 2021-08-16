# Denner Mobile API Spec

## Data and resources
The Denner Mobile Web Service provides data and functions for the Denner Mobile Apps.

### Stores

* `GET /stores` (Filialen, [example](examples/stores.json))
* `GET /store-filters` (Filialfilter, [example](examples/store-filters.json))

### Promotions

* `GET /featured-articles` (Startseitenartikel, [example](examples/featured-articles.json))
* `GET /online-filters` (Angebotsfilter, [example](examples/online-filters.json))
* `GET /online-filters/{id}/online-publications` (Werbemittel, [example](examples/online-publications.json))
* `GET /online-filters/{id}/online-groups` (Internet-Sortimente, [example](examples/online-groups.json))

### Banners

* `GET /banners` (Banner, [example](examples/banners.json))

## Documentation and Building 

To see the documentation page [Swagger UI](https://swagger.io/tools/swagger-ui/) visit  http://denner-mobile-api-docs.detailnet.ch/ or 
for development start the Docker instance that presents the static HTML pages in `/docs`  (`lando start` and then view http://denner-mobile-api-spec.detailnet.me/)

### Building
To build the specification we're using [swagger-codegen](https://github.com/swagger-api/swagger-codegen).

#### Using Ubuntu on WSL2 
Run the following commands to install swagger-codgen and it's dependencies in a separate directory:

        cd ..
        git clone git@github.com:swagger-api/swagger-codegen.git
        sudo apt-get install maven
        sudo apt install openjdk-11-jdk
        cd swagger-codegen
        git fetch origin 3.0.0:3.0.0
        git checkout 3.0.0
        #  export JDK_JAVA_OPTIONS=-Djdk.attach.allowAttachSelf=true .. not sure if really needed
        mvn clean package

#### JSON (used to update docs page too)
Once installed, `openapi.json` can be generated as follows:

        java -jar modules/swagger-codegen-cli/target/swagger-codegen-cli.jar generate \
            -i ../denner-mobile-api-spec/src/swagger.yml \
            -l openapi \
            -o ../denner-mobile-api-spec/docs
        
The file will be located at `docs/openapi.json`.

You can then review the changes in the local browser (`lando start` and then view http://denner-mobile-api-spec.detailnet.me/) and commit them.
