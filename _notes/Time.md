Do:

Whenever you are referring to an exact moment in time, persist the time according to a unified standard that is not affected by daylight savings. (GMT and UTC are equivalent with this regard, but it is preferred to use the term UTC. Notice that UTC is also known as Zulu or Z time.)

If instead you choose to persist a time using a local time value, include the local time offset for this particular time from UTC (this offset may change throughout the year), such that the timestamp can later be interpreted unambiguously.

In some cases, you may need to store both the UTC time and the equivalent local time. Often this is done with two separate fields, but some platforms support a datetimeoffset type that can store both in a single field.

When storing timestamps as a numeric value, use Unix time - which is the number of whole seconds since 1970-01-01T00:00:00Z (excluding leap seconds). If you require higher precision, use milliseconds instead. This value should always be based on UTC, without any time zone adjustment.
If you might later need to modify the timestamp, include the original time zone ID so you can determine if the offset may have changed from the original value recorded.

When scheduling future events, usually local time is preferred instead of UTC, as it is common for the offset to change. See answer, and blog post.
When storing whole dates, such as birthdays and anniversaries, do not convert to UTC or any other time zone.
When possible, store in a date-only data type that does not include a time of day.

If such a type is not available, be sure to always ignore the time-of-day when interpreting the value. If you cannot be assured that the time-of-day will be ignored, choose 12:00 Noon, rather than 00:00 Midnight as a more safe representative time on that day.
Remember that time zone offsets are not always an integer number of hours (for example, Indian Standard Time is UTC+05:30, and Nepal uses UTC+05:45).
If using Java, use java.time for Java 8 and later.
Much of that java.time functionality is back-ported to Java 6 & 7 in the ThreeTen-Backport library.
Further adapted for early Android (< 26) in the ThreeTenABP library.
These projects officially supplant the venerable Joda-Time, now in maintenance-mode. Joda-Time, ThreeTen-Backport, ThreeTen-Extra, java.time classes, and JSR 310 are led by the same man, Stephen Colebourne.
If using .NET, consider using Noda Time.
If using .NET without Noda Time, consider that DateTimeOffset is often a better choice than DateTime.
If using Perl, use DateTime.
If using Python, use pytz or dateutil.
If using JavaScript, use moment.js with the moment-timezone extension.
If using PHP > 5.2, use the native time zones conversions provided by DateTime, and DateTimeZone classes. Be careful when using DateTimeZone::listAbbreviations() - see answer. To keep PHP with up to date Olson data, install periodically the timezonedb PECL package; see answer.
If using C++, be sure to use a library that uses the properly implements the IANA timezone database. These include cctz, ICU, and Howard Hinnant's "tz" library.
Do not use Boost for time zone conversions. While its API claims to support standard IANA (aka "zoneinfo") identifiers, it crudely maps them to POSIX-style data, without considering the rich history of changes each zone may have had. (Also, the file has fallen out of maintenance.)
If using Rust, use chrono.
Most business rules use civil time, rather than UTC or GMT. Therefore, plan to convert UTC timestamps to a local time zone before applying application logic.
Remember that time zones and offsets are not fixed and may change. For instance, historically US and UK used the same dates to 'spring forward' and 'fall back'. However, in 2007 the US changed the dates that the clocks get changed on. This now means that for 48 weeks of the year the difference between London time and New York time is 5 hours and for 4 weeks (3 in the spring, 1 in the autumn) it is 4 hours. Be aware of items like this in any calculations that involve multiple zones.
Consider the type of time (actual event time, broadcast time, relative time, historical time, recurring time) what elements (timestamp, time zone offset and time zone name) you need to store for correct retrieval - see "Types of Time" in this answer.
Keep your OS, database and application tzdata files in sync, between themselves and the rest of the world.
On servers, set hardware clocks and OS clocks to UTC rather than a local time zone.
Regardless of the previous bullet point, server-side code, including web sites, should never expect the local time zone of the server to be anything in particular. see answer.
Prefer working with time zones on a case-by-case basis in your application code, rather than globally through config file settings or defaults.
Use NTP services on all servers.
If using FAT32, remember that timestamps are stored in local time, not UTC.
When dealing with recurring events (weekly TV show, for example), remember that the time changes with DST and will be different across time zones.
Always query date-time values as lower-bound inclusive, upper-bound exclusive (>=, <).
Don't:

Do not confuse a "time zone", such as America/New_York with a "time zone offset", such as -05:00. They are two different things. See the timezone tag wiki.
Do not use JavaScript's Date object to perform date and time calculations in older web browsers, as ECMAScript 5.1 and lower has a design flaw that may use daylight saving time incorrectly. (This was fixed in ECMAScript 6 / 2015).
Never trust the client's clock. It may very well be incorrect.
Don't tell people to "always use UTC everywhere". This widespread advice is shortsighted of several valid scenarios that are described earlier in this document. Instead, use the appropriate time reference for the data you are working with. (Timestamping can use UTC, but future time scheduling and date-only values should not.)
Testing:

When testing, make sure you test countries in the Western, Eastern, Northern and Southern hemispheres (in fact in each quarter of the globe, so 4 regions), with both DST in progress and not (gives 8), and a country that does not use DST (another 4 to cover all regions, making 12 in total).
Test transition of DST, i.e. when you are currently in summer time, select a time value from winter.
Test boundary cases, such as a timezone that is UTC+12, with DST, making the local time UTC+13 in summer and even places that are UTC+13 in winter
Test all third-party libraries and applications and make sure they handle time zone data correctly.
Test half-hour time zones, at least.
Reference:

The detailed timezone tag wiki page on Stack Overflow
Olson database, aka Tz_database
IETF draft procedures for maintaining the Olson database
Sources for Time Zone and DST
ISO format (ISO 8601)
Mapping between Olson database and Windows Time Zone Ids, from the Unicode Consortium
Time Zone page on Wikipedia
StackOverflow questions tagged dst
StackOverflow questions tagged timezone
Dealing with DST - Microsoft DateTime best practices
Network Time Protocol on Wikipedia
Other:

Lobby your representative to end the abomination that is DST. We can always hope...
Lobby for Earth Standard Time