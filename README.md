# Performance Improvement of OpenEdX

#Synopsis of the Project 

EdX is a MOOC(Massive Open Online Course) platform started by MIT and Harvard in collaboration for
revolutionizing online education. EdX is among the most popular MOOC’s in the world because of the
advance features it provides for making online education of student fruitful and more effective worldwide. It
also provides the author an effective way to design a course.
OpenEdX is the open source platform based on the EdX platform and is created on the Django framework
(written in python). RocksDB, a storage engine has been presented by Facebook Inc. as a better alternative to
InnoDB, both in terms of throughput and reduced storage space requirements.
The project deals with integration of MongoRocks and MyRocks, built by integrating RocksDB into
MongoDB and MySQL, respectively, in the OpenEdX framework and run benchmark tests to check for its
feasibility and viability.

#Product Scope

The OpenEdX system or platform provides an easy and effective way to build MOOC’s for students and
others to opt for free online courses. The benefits of this is that the traditional learning methods (like
classrooms with black boards) are upgraded with online interactive support using computers as a tool to
provide all kind of courses in interactive manner.
It also provides an interactive platform for the author to make/design a high quality online course with
different kinds of grading systems and other facilities.
Minimizing space amplification is important to efficient hardware use because storage space is the bottleneck
in production environments. SSDs process far fewer reads/s and writes/s during peak times under InnoDB
than what the hardware is capable of. The throughput level under InnoDB is low, not because of any
bottleneck on the SSD or the processing node — e.g., CPU utilization remains below 40% — but because the
query rate per node is low. RocksDB provides an efficient solution to this issue, under production conditions.
As a result it may be possible to use the same engine enabled database system for the OpenEdX framework,
thus enabling more efficient usage of disk space and faster execution time.