pg_repack -- Reorganize tables in OpenGauss 1.1.0 databases with minimal locks
=========================================================================

- Homepage: https://reorg.github.com/pg_repack
- Download: https://pgxn.org/dist/pg_repack/
- Development: https://github.com/reorg/pg_repack
- Bug Report: https://github.com/reorg/pg_repack/issues

For OpenGauss user
Bug Report:

-  https://github.com/lvhui465021/pg_repack
-  hui.lv@enmotech.com
-  wei.liu@enmotech.com

|travis|

.. |travis| image:: https://travis-ci.org/reorg/pg_repack.svg?branch=master
    :target: https://travis-ci.org/reorg/pg_repack
    :alt: Linux and OSX build status

pg_repack_ is a OpenGauss 1.1.0 extension which lets you remove bloat from
tables and indexes, and optionally restore the physical order of clustered
indexes. Unlike CLUSTER_ and `VACUUM FULL`_ it works online, without
holding an exclusive lock on the processed tables during processing.
pg_repack is efficient to boot, with performance comparable to using
CLUSTER directly.

Please check the documentation (in the ``doc`` directory or online_) for
installation and usage instructions.

.. _pg_repack: https://reorg.github.com/pg_repack
.. _CLUSTER: https://www.postgresql.org/docs/current/static/sql-cluster.html
.. _VACUUM FULL: VACUUM_
.. _VACUUM: https://www.postgresql.org/docs/current/static/sql-vacuum.html
.. _online: pg_repack_
.. _issue: https://github.com/reorg/pg_repack/issues/23


What about pg_reorg?
--------------------

pg_repack is a fork of the pg_reorg_ project, which has proven hugely
successful. Unfortunately new feature development on pg_reorg_ has slowed
or stopped since late 2011.

pg_repack was initially released as a drop-in replacement for pg_reorg,
addressing some of the shortcomings of the last pg_reorg version (such as
support for PostgreSQL 9.2 and EXTENSION packaging) and known bugs.

pg_repack 1.2 introduces further new features (parallel index builds,
ability to rebuild only indexes) and bugfixes. In some cases its behaviour
may be different from the 1.1.x release so it shouldn't be considered a
drop-in replacement: you are advised to check the documentation__ before
upgrading from previous versions.

.. __: pg_repack_
.. _pg_reorg: https://github.com/reorg/pg_reorg


Methods of compiling
---------------------

1. add the environment variables the PATH of the OpenGauss 1.1.0 executable program directory into $PATH.
2. make.
3. make install.

generate the pg_repack executable program in pg_repack/bin/pg_repack and dynamic library pg_repack.so in pg_repack/lib/pg_repack.so.

when compile the OpenGauss 1.1.0, set the environment variables:

CODE_BASE=path/openGauss-server
                                                                     assign the OpenGauss 1.1.0 code directory to CODE_BASE
BINARYLIBS=path/openGauss-third_party_binarylibs
                                                                     assign the OpenGauss 1.1.0 third binarylibs to BINARYLIBS
GAUSSHOME=path/opengauss_install_path
                                                                     assign the OpenGauss 1.1.0 install directory to GAUSSHOME
CC=$BINARYLIBS/buildtools/centos7.6_x86_64/gcc7.3/gcc/bin/gcc
                                                                     assign the gcc version, because the OpenGauss 1.1.0 need gcc7.3
CXX=$BINARYLIBS/buildtools/centos7.6_x86_64/gcc7.3/gcc/bin/g++
                                                                     assign the g++ version, because the OpenGauss 1.1.0 need g++7.3
LD_LIBRARY_PATH=$GAUSSHOME/lib:$GCC_PATH/gcc/lib64:$GCC_PATH/mpc/lib:$GCC_PATH/mpfr/lib:$GCC_PATH/gmp/lib:$BINARYLIBS/dependency/centos7.6_x86_64/openssl/comm/lib:$BINARAYLIBS/dependency/centos7.6_x86_64/libobs/comm/lib:$BINARYLIBS/dependency/centos7.6_x86_64/grpc/comm/lib:$LD_LIBRARY_PATH
                                                                     assign the dynamic library path when compile OpenGauss 1.1.0
PATH=$GCC_PATH/gcc/bin:$PATH
                                                                     assign the gcc executable program directory

Download the openGauss-third_party_binarylibs from there_.
From the following website, you can obtain the binarylibs we have compiled. Please unzip it and rename to binarylibs after you download.
https://opengauss.obs.cn-south-1.myhuaweicloud.com/1.1.0/openGauss-third_party_binarylibs.tar.gz

.. _there: https://opengauss.obs.cn-south-1.myhuaweicloud.com/1.1.0/openGauss-third_party_binarylibs.tar.gz
