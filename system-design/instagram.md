# 1. Requirements

**Functional Requirements**

1. Users should be able to upload/download/view photos.
2. Users can perform searches based on photo/video titles.
3. Users can follow other users.
4. The system should be able to generate and display a user’s timeline consisting of top photos from all the people the user follows.

**Non-functional Requirements**

1. Our service needs to be highly available.
2. The acceptable latency of the system is 200ms for timeline generation.
3. Consistency can take a hit \(in the interest of availability\), if a user doesn’t see a photo for a while, it should be fine.
4. The system should be highly reliable, any photo/video uploaded should not be lost.

**Not in scope:**Adding tags to photos, searching photos on tags, commenting on photos, tagging users to photos, who to follow, suggestions, etc.

# 2. Capacity

* Let’s assume we have 300M total users, with 1M daily active users.

* 2M new photos every day, 23 new photos every second.

* Average photo file size =&gt; 200KB

* Total space required for 1 day of photos: 2M \* 200KB =&gt; 400 GB
* Total space required for 5 years: 400GB \* 365 \(days a year\) \* 5 \(years\) ~= 712 TB



