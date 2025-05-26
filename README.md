## 1.What is PostgreSQL?
## Answer: 
PostgreSQL হল একটি ওপেন-সোর্স রিলেশনাল ডেটাবেইজ ম্যানেজমেন্ট সিস্টেম (RDBMS) যা SQL সমর্থন করে। এটি রিলেশনাল ডাটাবেস মডেল অনুসরণ করে, সারি এবং কলাম সহ টেবিলে ডেটা সংগঠিত করে এবং টেবিলের মধ্যে সম্পর্ক তৈরি করে।এটি ACID (Atomicity, Consistency, Isolation, Durability) বৈশিষ্ট্যগুলি সমর্থন করে |

## 2. What is the purpose of a database schema in PostgreSQL?
## Answer:
PostgreSQL-এ ডেটাবেস স্কিমা (Schema) হলো একটি সংগঠিত কাঠামো যা একই ডেটাবেইজের মধ্যে বিভিন্ন টেবিল, ভিউ, ফাংশন ইত্যাদি আলাদা রাখতে সাহায্য করে।এটি ডেটাবেস অবজেক্টগুলিকে সুসংগঠিতভাবে সাজাতে সাহায্য করে, বিশেষ করে যখন একটি ডেটাবেসে অনেক টেবিল থাকে বা একাধিক অ্যাপ্লিকেশন একই ডেটাবেস ব্যবহার করে।বিভিন্ন স্কিমাতে একই নামের অবজেক্ট থাকতে পারে|Example:  `public.users` এবং `app.users` উভয়ই একই ডেটাবেসে থাকতে পারে|

## 3.Explain the Primary Key and Foreign Key concepts in PostgreSQL.
## Answer: 
Primary Key হলো একটি কলাম বা কলামের সেট যা একটি টেবিলের প্রতিটি সারিকে Unique ভাবে শনাক্ত করে। Primary Key কলামের প্রতিটি মান অবশ্যই Unique হতে হবে। কোনো দুটি সারির Primary Key মান একই হতে পারবে না এবং Null হতে পারবে না|একটি টেবিলের শুধুমাত্র Primary Key থাকতে পারে| Example:  `rangers` টেবিলের `ranger_id` কলামটি একটি Primary Key, কারণ প্রতিটি `ranger` এর একটি অনন্য আইডি আছে এবং এটি নাল হতে পারে না।
Foreign Key হলো এমন একটি মাধ্যম যা অন্য একটি টেবিলের Primary Key এর সঙ্গে সম্পর্কিত, এবং এটি অন্য টেবিলের সাথে রিলেশন তৈরি করতে ব্যবহৃত হয়।এবং Referential integrity বজায় রাখে ,যার মানে Child টেবিলের Foreign Key কলামে এমন কোনো মান থাকতে পারবে না যা Parent টেবিলের সংশ্লিষ্ট Primary Key কলামে বিদ্যমান নেই। Example: `sightings` টেবিলের `ranger_id` এবং `species_id` কলামগুলি ফরেন কী। `ranger_id` `rangers` টেবিলের `ranger_id` কে রেফারেন্স করে এবং `species_id` `species` টেবিলের `species_id` কে Reference করে।

## 4.What is the difference between the VARCHAR and CHAR data types?
## Answer:
VARCHER এটি একটি String ডেটা টাইপ|এটি পরিবর্তনশীল মেমরি ব্যবহার করে।`VARCHAR(n)`যদি ইনপুট String `n` অক্ষরের চেয়ে ছোট হয়, তবে এটি প্যাড করা হয় না।এটি প্রতিটি অক্ষরের জন্য ১ বাইট এবং দৈর্ঘ্যের তথ্য ধরে রাখার জন্য কিছু অতিরিক্ত বাইট নেয়।এটি পরিবর্তনশীল দৈর্ঘ্যের স্ট্রিংয়ের জন্য সবচেয়ে বেশি ব্যবহৃত হয়| Example: নাম, ঠিকানা, বিবরণ।
CHAR ও হলো একটি String ডেটা টাইপ|এটি নির্দিষ্ট মেমরি ব্যবহার করে|`CHAR` ছোট স্ট্রিংগুলিকে স্পেস দিয়ে প্যাড করে|এটি প্রতিটি অক্ষরের জন্য ১ বাইট নেয় এবং এটি সাধারণত স্থির দৈর্ঘ্যের ডেটার জন্য ব্যবহৃত হয়|

## 5.What are the LIMIT and OFFSET clauses used for?
## Answer:
LIMIT clauses এটি query ফলাফল সেট থেকে কতগুলি সারি ফেরত দেওয়া হবে তা সীমাবদ্ধ করে। এটি query শেষে যুক্ত হয়।Example:
SELECT common_name, sighting_time
FROM sightings
JOIN species ON sightings.species_id = species.species_id
ORDER BY sighting_time DESC
LIMIT 2;
এই Query টি sightings এবং species টেবিল থেকে সবচেয়ে সাম্প্রতিক দুটি সাইটিং দেখাবে।
OFFSET clauses এটি ফলাফল সেটের শুরু থেকে কতগুলি সারি বাদ দেওয়া হবে তা নির্দিষ্ট করে। এটি LIMIT ক্লজের সাথে ব্যবহার করা হয়।Example:
SELECT "name"
FROM rangers
ORDER BY "name"
LIMIT 2 OFFSET 2;
এই Query টি rangers টেবিল থেকে name অনুসারে সাজানো 3rd,4th name ফেরত দেবে। প্রথম 2টি সারি বাদ দিয়ে পরবর্তী 2টি সারি দেখাবে।

