창업진흥원 K-Startup WEB,WAS 현황
=================================

author: 이미나 (mina@techware.co.kr), date: 2022-06-03
''''''''''''''''''''''''''''''''''''''''''''''''''''''

1. 서버 정보 (Hostname)
-----------------------

운영 서버

-  Active

   -  Apache: KSTPRDWEB01, KSTPRDWEB02, KSTPRDWEB03
   -  Tomcat: KSTPRDWAS01, KSTPRDWAS02, KSTPRDWAS03

-  Standby

   -  Apache: KSTPRDWEB04, KSTPRDWAS05, KSTPRDWEB06
   -  Tomcat: KSTPRDWAS04, KSTPRDWAS05, KSTPRDWAS06

개발 서버

-  Apache: KSTDEVWEB
-  Tomcat: KSTDEVWAS

2. Apache
---------

2.1 설치 정보
~~~~~~~~~~~~~

+---------------+-----------------------------------------------------+
| 설치 정보     | 내용                                                |
+===============+=====================================================+
| 아파치 버전   | 2.4.53                                              |
+---------------+-----------------------------------------------------+
| 설치 경로     | /DATA/apache                                        |
+---------------+-----------------------------------------------------+
| 설치 계정     | apache:apache                                       |
+---------------+-----------------------------------------------------+
| 프로세스 계정 | apache                                              |
+---------------+-----------------------------------------------------+
| 로그 경로     | /LOG/apache                                         |
+---------------+-----------------------------------------------------+
| 명령어        | 시작: ``sudo systemctl start apache`` 종료:         |
|               | ``sudo systemctl stop apache``                      |
+---------------+-----------------------------------------------------+
| Listen 포트   | 80, 8081, 8082, 8084, 10422                         |
+---------------+-----------------------------------------------------+

2.2 mod_jk (Tomcat Connector)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

2.2.1 workers.properties - **Worker**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

KSTPRDWEB01 ~ KSTPRDWEB03 (Active)
''''''''''''''''''''''''''''''''''

+-----------+-----------+-----------+-----------+-----------+-----------+
| Property  | was1      | was1_n    | was1_n    | wa        | eduwa     |
|           | _node10wa | ode20was2 | ode30was2 | s1_node50 | s1eduwas2 |
|           | s2_node10 | _node20wa | _node30wa |           |           |
|           | wa        | s3_node20 | s3_node30 |           |           |
|           | s3_node10 |           |           |           |           |
+===========+===========+===========+===========+===========+===========+
| host      | 192.18    | 192.18    | 192.18    | 192.1     | 192       |
|           | 6.111.411 | 6.111.411 | 6.111.411 | 68.111.41 | .168.111. |
|           | 92.186.11 | 92.186.11 | 92.186.11 |           | 201192.16 |
|           | 1.42192.1 | 1.42192.1 | 1.42192.1 |           | 8.111.202 |
|           | 86.111.43 | 86.111.43 | 86.111.43 |           |           |
+-----------+-----------+-----------+-----------+-----------+-----------+
| port      | 8009      | 8109      | 8209      | 8409      | 8009      |
+-----------+-----------+-----------+-----------+-----------+-----------+
| type      | ajp13     | ajp13     | ajp13     | ajp13     | ajp13     |
+-----------+-----------+-----------+-----------+-----------+-----------+
| lbfactor  | 1         | 1         | 1         | 1         | 1         |
+-----------+-----------+-----------+-----------+-----------+-----------+
| socke     | 0         | 0         | 0         | 0         | 0         |
| t_timeout |           |           |           |           |           |
+-----------+-----------+-----------+-----------+-----------+-----------+
| socket_   | true      | true      | true      | true      | true      |
| keepalive |           |           |           |           |           |
+-----------+-----------+-----------+-----------+-----------+-----------+

KSTPRDWEB04 ~ KSTPRDWEB06 (Standby)
'''''''''''''''''''''''''''''''''''

+-----------+-----------+-----------+-----------+-----------+-----------+
| Property  | was1      | was1_n    | was1_n    | wa        | eduwa     |
|           | _node10wa | ode20was2 | ode30was2 | s1_node50 | s1eduwas2 |
|           | s2_node10 | _node20wa | _node30wa |           |           |
|           | wa        | s3_node20 | s3_node30 |           |           |
|           | s3_node10 |           |           |           |           |
+===========+===========+===========+===========+===========+===========+
| host      | 192.18    | 192.18    | 192.18    | 192.1     | 192       |
|           | 6.111.411 | 6.111.411 | 6.111.411 | 68.111.41 | .168.111. |
|           | 92.186.11 | 92.186.11 | 92.186.11 |           | 201192.16 |
|           | 1.42192.1 | 1.42192.1 | 1.42192.1 |           | 8.111.202 |
|           | 86.111.43 | 86.111.43 | 86.111.43 |           |           |
+-----------+-----------+-----------+-----------+-----------+-----------+
| port      | 8009      | 8109      | 8209      | 8409      | 8009      |
+-----------+-----------+-----------+-----------+-----------+-----------+
| type      | ajp13     | ajp13     | ajp13     | ajp13     | ajp13     |
+-----------+-----------+-----------+-----------+-----------+-----------+
| lbfactor  | 1         | 1         | 1         | 1         | 1         |
+-----------+-----------+-----------+-----------+-----------+-----------+
| socke     | 0         | 0         | 0         | 0         | 0         |
| t_timeout |           |           |           |           |           |
+-----------+-----------+-----------+-----------+-----------+-----------+
| socket_   | true      | true      | true      | true      | true      |
| keepalive |           |           |           |           |           |
+-----------+-----------+-----------+-----------+-----------+-----------+

2.2.2 workers.properties - **Load Balancer**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _kstprdweb01-kstprdweb03-active-1:

KSTPRDWEB01 ~ KSTPRDWEB03 (Active)
''''''''''''''''''''''''''''''''''

+-------------+-------------+-------------+-------------+-------------+
| Property    | wlb_node10  | wlb_node20  | wlb_node30  | eduwlb      |
+=============+=============+=============+=============+=============+
| bala        | was1_node10 | was1_node20 | was1_node30 | edu         |
| nce_workers | was2_node10 | was2_node20 | was2_node30 | was1eduwas2 |
|             | was3_node10 | was3_node20 | was3_node30 |             |
+-------------+-------------+-------------+-------------+-------------+
| type        | lb          | lb          | lb          | lb          |
+-------------+-------------+-------------+-------------+-------------+
| retries     | 2           | 2           | 2           | 2           |
+-------------+-------------+-------------+-------------+-------------+
| method      | S           | S           | S           | (R)         |
+-------------+-------------+-------------+-------------+-------------+
| sti         | true        | true        | true        | (true)      |
| cky_session |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| set_ses     | true        | true        | true        | (false)     |
| sion_cookie |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| ses         | US          | MNGR        | USR         | (           |
| sion_cookie | R_JESSIONID | _JSESSIONID | _JSESSIONID | JSESSIONID) |
+-------------+-------------+-------------+-------------+-------------+

KSTPRDWEB01 ~ KSTPRDWEB03 (Standby)
'''''''''''''''''''''''''''''''''''

+-------------+-------------+-------------+-------------+-------------+
| Property    | wlb_node10  | wlb_node20  | wlb_node30  | eduwlb      |
+=============+=============+=============+=============+=============+
| bala        | was1_node10 | was1_node20 | was1_node30 | edu         |
| nce_workers | was2_node10 | was2_node20 | was2_node30 | was1eduwas2 |
|             | was3_node10 | was3_node20 | was3_node30 |             |
+-------------+-------------+-------------+-------------+-------------+
| type        | lb          | lb          | lb          | lb          |
+-------------+-------------+-------------+-------------+-------------+
| retries     | 2           | 2           | 2           | 2           |
+-------------+-------------+-------------+-------------+-------------+
| method      | S           | S           | S           | (R)         |
+-------------+-------------+-------------+-------------+-------------+
| sti         | true        | true        | true        | (true)      |
| cky_session |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| set_ses     | true        | true        | true        | (false)     |
| sion_cookie |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| ses         | US          | MNGR        | USR         | (           |
| sion_cookie | R_JESSIONID | _JSESSIONID | _JSESSIONID | JSESSIONID) |
+-------------+-------------+-------------+-------------+-------------+

2.3 Virtual Host
~~~~~~~~~~~~~~~~

.. _kstprdweb01-kstprdweb03-active-2:

KSTPRDWEB01 ~ KSTPRDWEB03 (Active)
''''''''''''''''''''''''''''''''''

.. raw:: html

   <table>

.. raw:: html

   <thead>

.. raw:: html

   <tr>

.. raw:: html

   <th>

Property

.. raw:: html

   </th>

.. raw:: html

   <th>

.. container::

   \*:80

.. raw:: html

   </th>

.. raw:: html

   <th>

.. container::

   \*:8081

.. raw:: html

   </th>

.. raw:: html

   <th>

.. container::

   \*:8082

.. raw:: html

   </th>

.. raw:: html

   <th>

.. container::

   \*:8084

.. raw:: html

   </th>

.. raw:: html

   <th>

.. container::

   \*:10422

.. raw:: html

   </th>

.. raw:: html

   </tr>

.. raw:: html

   </thead>

.. raw:: html

   <tbody>

.. raw:: html

   <tr>

.. raw:: html

   <th>

ServerName

.. raw:: html

   </th>

.. raw:: html

   <td>

www.k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

www.k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

www.k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

www.k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

center.k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <th>

ServerAlias

.. raw:: html

   </th>

.. raw:: html

   <td>

k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <th>

JkMount

.. raw:: html

   </th>

.. raw:: html

   <td>

/\* wlb_node10/ccei/\* was1_node50/edu/\* edulb

.. raw:: html

   </td>

.. raw:: html

   <td>

/\* wlb_node20

.. raw:: html

   </td>

.. raw:: html

   <td>

/\* wlb_node30

.. raw:: html

   </td>

.. raw:: html

   <td>

/\* wlb_node50

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <th>

JkUnMount

.. raw:: html

   </th>

.. raw:: html

   <td>

/cbc/\* wlb_node10

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <th>

RewriteCondRewriteRule

.. raw:: html

   </th>

.. raw:: html

   <td colspan="4">

RewriteCond %{HTTP_HOST} !^www.(.*)$ [NC]RewriteRule ^(.*)$
https://www.%{HTTP_HOST}/$1 [R=301,L]RewriteCond
%{HTTP:X-Forwarded-Proto} !=httpsRewriteCond %{REQUEST_URI}
!^/cbc/version/version.ini$RewriteRule .\*
https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <th>

Log Path

.. raw:: html

   </th>

.. raw:: html

   <td>

/LOG/apache/USER

.. raw:: html

   </td>

.. raw:: html

   <td>

/LOG/apache/MNGR

.. raw:: html

   </td>

.. raw:: html

   <td>

/LOG/apache/CNTR-MNGR

.. raw:: html

   </td>

.. raw:: html

   <td>

LOG/apache/CCEI

.. raw:: html

   </td>

.. raw:: html

   <td>

/LOG/apache/KCENTER

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <th>

ProxyPass

.. raw:: html

   </th>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

/ ws://192.168.111.41:10422/

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </tbody>

.. raw:: html

   </table>

.. _kstprdweb04-kstprdweb06-standby-1:

KSTPRDWEB04 ~ KSTPRDWEB06 (Standby)
'''''''''''''''''''''''''''''''''''

.. raw:: html

   <table>

.. raw:: html

   <thead>

.. raw:: html

   <tr>

.. raw:: html

   <th>

Property

.. raw:: html

   </th>

.. raw:: html

   <th>

.. container::

   \*:80

.. raw:: html

   </th>

.. raw:: html

   <th>

.. container::

   \*:8081

.. raw:: html

   </th>

.. raw:: html

   <th>

.. container::

   \*:8082

.. raw:: html

   </th>

.. raw:: html

   <th>

.. container::

   \*:8084

.. raw:: html

   </th>

.. raw:: html

   <th>

.. container::

   \*:10422

.. raw:: html

   </th>

.. raw:: html

   </tr>

.. raw:: html

   </thead>

.. raw:: html

   <tbody>

.. raw:: html

   <tr>

.. raw:: html

   <th>

ServerName

.. raw:: html

   </th>

.. raw:: html

   <td>

www.k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

www.k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

www.k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

www.k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

center.k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <th>

ServerAlias

.. raw:: html

   </th>

.. raw:: html

   <td>

k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

k-startup.go.kr

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <th>

JkMount

.. raw:: html

   </th>

.. raw:: html

   <td>

/\* wlb_node10/ccei/\* was1_node50/edu/\* edulb

.. raw:: html

   </td>

.. raw:: html

   <td>

/\* wlb_node20

.. raw:: html

   </td>

.. raw:: html

   <td>

/\* wlb_node30

.. raw:: html

   </td>

.. raw:: html

   <td>

/\* wlb_node50

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <th>

JkUnMount

.. raw:: html

   </th>

.. raw:: html

   <td>

/cbc/\* wlb_node10

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <th>

RewriteCondRewriteRule

.. raw:: html

   </th>

.. raw:: html

   <td colspan="4">

RewriteCond %{HTTP_HOST} !^www.(.*)$ [NC]RewriteRule ^(.*)$
https://www.%{HTTP_HOST}/$1 [R=301,L]RewriteCond
%{HTTP:X-Forwarded-Proto} !=httpsRewriteCond %{REQUEST_URI}
!^/cbc/version/version.ini$RewriteRule .\*
https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <th>

Log Path

.. raw:: html

   </th>

.. raw:: html

   <td>

/LOG/apache/USER

.. raw:: html

   </td>

.. raw:: html

   <td>

/LOG/apache/MNGR

.. raw:: html

   </td>

.. raw:: html

   <td>

/LOG/apache/CNTR-MNGR

.. raw:: html

   </td>

.. raw:: html

   <td>

LOG/apache/CCEI

.. raw:: html

   </td>

.. raw:: html

   <td>

/LOG/apache/KCENTER

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <th>

ProxyPass

.. raw:: html

   </th>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   <td>

/ ws://192.168.111.41:10422/

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </tbody>

.. raw:: html

   </table>

3. Tomcat
---------

+--------------------------+------------------------------------------+
| 설치 정보                | 내용                                     |
+==========================+==========================================+
| Tomcat 버전              | 9                                        |
+--------------------------+------------------------------------------+
| 설치 경로(CATALINA_HOME) | /DATA/tomcat                             |
+--------------------------+------------------------------------------+
| 설치 계정                | tomcat:tomcat                            |
+--------------------------+------------------------------------------+
| JAVA_HOME                | /usr/lib/jvm/java-1.                     |
|                          | 8.0-openjdk-1.8.0.302.b08-0.el7_9.x86_64 |
+--------------------------+------------------------------------------+
| 명령어                   | 시작: ``sudo systemctl start apache``    |
|                          | 종료: ``sudo systemctl stop apache``     |
+--------------------------+------------------------------------------+
| Instance                 | node10, node20, node30,                  |
|                          | node50(KSTPRDWAS01)                      |
+--------------------------+------------------------------------------+

3.1 Instance 정보
~~~~~~~~~~~~~~~~~

KSTPRDWAS01 ~ KSTPRDWAS03 (Active)
''''''''''''''''''''''''''''''''''

+-------------+-------------+-------------+-------------+-------------+
| Property    | node10      | node20      | node30      | node50      |
+=============+=============+=============+=============+=============+
| Host        | KSTPRDWAS01 | KSTPRDWAS01 | KSTPRDWAS01 | KSTPRDWAS01 |
|             | KSTPRDWAS02 | KSTPRDWAS02 | KSTPRDWAS02 |             |
|             | KSTPRDWAS03 | KSTPRDWAS03 | KSTPRDWAS03 |             |
+-------------+-------------+-------------+-------------+-------------+
| CA          | /           | /           | /           | /           |
| TALINA_BASE | DATA/tomcat | DATA/tomcat | DATA/tomcat | DATA/tomcat |
+-------------+-------------+-------------+-------------+-------------+
| DocBase     | /DAT        | /DATA/      | /DATA/ROOT  | /DATA/ROOT  |
|             | A/ROOT/USER | ROOT/CENTER |             |             |
+-------------+-------------+-------------+-------------+-------------+
| JVM         | -           | -           | -           | -           |
+-------------+-------------+-------------+-------------+-------------+
| LOGHOME     | -           | -           | -           | -           |
+-------------+-------------+-------------+-------------+-------------+
| Max         | -           | -           | -           | -           |
| Connections |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| Session     | -           | -           | -           | -           |
| Threads     |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| Context     | -           | -           | -           | -           |
| Path        |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| Command     | -           | -           | -           | -           |
+-------------+-------------+-------------+-------------+-------------+
| Sessio      | -           | -           | -           | -           |
| nCookieName |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| JvmRoute    | -           | -           | -           | -           |
+-------------+-------------+-------------+-------------+-------------+

.. _kstprdwas01-kstprdwas03-active-1:

KSTPRDWAS01 ~ KSTPRDWAS03 (Active)
''''''''''''''''''''''''''''''''''

+-------------+-------------+-------------+-------------+-------------+
| Property    | node10      | node20      | node30      | node50      |
+=============+=============+=============+=============+=============+
| Host        | KSTPRDWAS01 | KSTPRDWAS01 | KSTPRDWAS01 | KSTPRDWAS01 |
|             | KSTPRDWAS02 | KSTPRDWAS02 | KSTPRDWAS02 |             |
|             | KSTPRDWAS03 | KSTPRDWAS03 | KSTPRDWAS03 |             |
+-------------+-------------+-------------+-------------+-------------+
| CA          | /           | /           | /           | /           |
| TALINA_BASE | DATA/tomcat | DATA/tomcat | DATA/tomcat | DATA/tomcat |
+-------------+-------------+-------------+-------------+-------------+
| DocBase     | /DAT        | /DATA/      | /DATA/ROOT  | /DATA/ROOT  |
|             | A/ROOT/USER | ROOT/CENTER |             |             |
+-------------+-------------+-------------+-------------+-------------+
| JVM         | -           | -           | -           | -           |
+-------------+-------------+-------------+-------------+-------------+
| LOGHOME     | -           | -           | -           | -           |
+-------------+-------------+-------------+-------------+-------------+
| Max         | -           | -           | -           | -           |
| Connections |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| Session     | -           | -           | -           | -           |
| Threads     |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| Context     | -           | -           | -           | -           |
| Path        |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| Command     | -           | -           | -           | -           |
+-------------+-------------+-------------+-------------+-------------+
| Sessio      | -           | -           | -           | -           |
| nCookieName |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| JvmRoute    | -           | -           | -           | -           |
+-------------+-------------+-------------+-------------+-------------+

그 외 node10 설정: context.xml

.. code:: xml

   <Resources>
   </Resources>

3.2 Session Cluster
~~~~~~~~~~~~~~~~~~~

============ ================ =============
cluster port server           node
============ ================ =============
4000         was1, was2, was3 node10,node30
4001         was1, was2, was3 node20
4002         was1, was2, was3 node10,node30
============ ================ =============

