linux
**************


awk
=======

sed
========


grep
========


shell mac
==================

命令如下::

    linux下的命令：

    find ./target/generated-sources/ -name “*.java” | xargs -n1 -i cp {} ./src/main/java/com/grpc/mistra/generate/

    其在mac下的等价命令为：

    find ./target/generated-sources/ -name “*.java” | xargs -n1 -I F cp “F” ./src/main/java/com/grpc/mistra/generate/

    也就是说 -i {}等价于-I F “F”

    find . -name "README.rst" | xargs -I F mv F .gitkeep


