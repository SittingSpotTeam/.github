# Sitting Spot

![Architecture](https://drive.google.com/uc?id=1zdPsijnLdop0RNGODiwsK2JCv_GjBfz1)


## Demo deploy

To deploy a demo of the service, first clone the [deploy repository](https://github.com/SittingSpotTeam/deploy).
Then navigate to the `dockercompose` folder and run `docker-compose -f sittingspot-compose.yaml`.
Note: be sure to have ports from 8080 to 8090 free to deploy the application.

## API

This section will assume that the deploy has been conducted with the instructions in the section above, so each service is reacheable from localhost given the correct port.

- moderationservice -> 8080
- queryoptimizer -> 8082
- reviewdatalayer -> 8083
- reviewprocesslayer -> 8084
- searchadapter -> 8085
- searchprocesslayer -> 8086
- searchservice -> 8087
- sittingspotdatalayer -> 8088
- tagextractor -> 8089
- querydatalayer -> 8090

Each service has in its repository an `api.yaml` file with a more formal definition of its APIs.

### searchprocesslayer

[api](https://github.com/SittingSpotTeam/SearchProcessLayer/blob/main/api.yaml)

#### GET host/api/v1/?x={longitude}&y={latutide}&area={r_area}

Allow to search for sitting spots in a given area with center (latutude,longitude), the radius of the area searched is r_area.
Will also update the query db with the result obtained.

### reviewprocesslayer

[api](https://github.com/SittingSpotTeam/ReviewProcessLayer/blob/main/api.yaml)

#### GET host/api/v1?id={sitting_spot_id}

Retrieves the reviews of the sitting spot with id sitting_spot_id.

#### POST host/api/v1/{sitting_spot_id}

Allow to create a new review on the sitting spot with id sitting_spot_id, the content of the review has to be in the body of the request as a simple string.


### searchservice

[api](https://github.com/SittingSpotTeam/SearchService/blob/main/api.yaml)

#### GET host/api/v1?x={longitude}&y={latutide}&area={r_area}

Forward the request to queryoptimizer to get a past result so to avoid querying external services.
If no result was found will forward the requst to searchadapter.

### searchadapter

[api](https://github.com/SittingSpotTeam/SearchAdapter/blob/main/api.yaml)

#### GET host/api/v1?x={longitude}&y={latutide}&area={r_area}

Will query external services and the internal data layer for sitting spots in the area requested.
Will also update the internal data layer with new sitting spots.

### sittingspotdatalayer

[api](https://github.com/SittingSpotTeam/SittingSpotDataLayer/blob/main/api.yaml)

#### GET host/api/v1

Retrieve all the sitting spots.

#### POST host/api/v1

Add a new sitting spot. 
refer to `api.yaml` of SittingSpotDataLayer for the format of the body of the request.

#### GET host/api/v1/{id}

Retrieve sitting spot with the specified id.

#### PUT host/api/v1/{id}

Allow to add user-defined (extracted from reviews) labels.

#### GET host/api/v1/find?x={longitude}&y={latutide}&area={r_area}

Retrieve sitting spots in the given area.

### queryoptimizer

[api](https://github.com/SittingSpotTeam/QueryOptimizer/blob/main/api.yaml)

#### GET host/api/v1?x={longitude}&y={latutide}&area={r_area}

Get from the query data layer all the past queries that searched spots inside the area specified.
If it finds any it will aggregate the results removing duplicates and return it.

### querydatalayer

[api](https://github.com/SittingSpotTeam/QueryDataLayer/blob/main/api.yaml)

#### GET host/api/v1?x={longitude}&y={latutide}&area={r_area}

Retrieve queries that searched spots inside the area specified.

#### POST host/api/v1

Add a new query with respective result.

### tagextractor

[api](https://github.com/SittingSpotTeam/TagExtractor/blob/main/api.yaml)

#### POST host/api/v1/{id}

Extract from the content of a review possible labels to be assigned to a sitting spot, and update the entry in sitting spot data layer.

### moderationservice

[api](https://github.com/SittingSpotTeam/ModerationService/blob/main/api.yaml)

#### POST host/api/v1

Given the content of a review (as a string in the body of the request) returns a string with censured bits.

### reviewdatalayer

[api](https://github.com/SittingSpotTeam/ReviewDataLayer/blob/main/api.yaml)

#### GET host/api/v1?id={id}

Retrieve all the reviews of the sitting spot with the id specified.

#### POST host/api/v1

Add a new review relative to a sitting spot.
