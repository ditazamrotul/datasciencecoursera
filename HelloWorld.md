## Datastore Statistics

Firestore in Datastore mode maintains statistics about the data stored for an application, such as how many entities there are of a given kind, or how much space is used by property values of a given type. You can view these statistics in the Cloud Console. Either open the Dashboard page or run a GQL query in the form of SELECT * FROM __Stat_Kind__ from the Entities page.

You can also access these values programmatically within the application by querying for specially named entities using the Datastore API. Each statistic is accessible as an entity whose kind name begins and ends with two underscores. For example, each app has exactly one entity of the kind __Stat_Total__ that represents statistics about all of the entities in Datastore mode in total. Each statistic entity has the following properties:

    count, the number of items considered by the statistic (a long integer)
    bytes, the total size of the items for this statistic (a long integer)
    timestamp, the time of the most recent update to the statistic (a date-time value)

Some statistic kinds also have additional properties, listed below.

When the statistics system creates new statistic entities, it does not delete the old statistic entities right away. The best way to get a consistent view of the statistics is to query for the statistic entity with the most recent timestamp, then use that timestamp value as a filter when fetching other statistic entities.

The statistic entities are included in the calculated statistic values. Statistic entities take up space relative to the number of unique kinds and property names used by the application.

The statistics system will also create statistics specific to each namespace. Note that if an application does not use namespaces, then namespace specific statistics will not be created. Namespace specific stats are found in the namespace that they're specific to. The kind names for namespace specific stats are prefixed with __Stat_Ns_ and have the same corresponding suffix as application wide statistics kinds.

Source:
https://cloud.google.com/datastore/docs/concepts/stats
