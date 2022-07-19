Contents of this docker-compose
===============================

This stack is to use serialization features. It is comprised of:
- an origin enterprise Metabase instance exposed in port 3001
- an origin postgres database as the application database of origin Metabase (not exposed, only seen by origin Metabase)
- a destination enterprise Metabase instance exposed in port 3002
- a destination postgres as the application database of destination Metabase (not exposed, only seen by destination Metabase)

The origin and destination Metabase applications see the folder "metabase_dump" that is the one where the origin dumps the data and the destination picks it up

Each stack (origin Metabase and destination Metabase) is on its own network (called metanet1 for origin and metanet2 for destination) so they are both isolated.

Serialization
=============

When you finish doing the questions/dashboards on the source instance (localhost:3001), from the command line do `docker exec -it metabase_origin java -jar /app/metabase.jar dump /target` to do the load from the source container and then `docker exec -it metabase_destination java -jar /app/metabase.jar load /target`