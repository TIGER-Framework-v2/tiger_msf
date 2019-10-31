# tiger_msf
TIGER Metasploit Framework tests execution container

### Environment Variables
`TEST_RESOURCE_FILE_LINK` contains link on resource file for *msfconsole* in raw format

### Commands to build
`docker build --build-arg msf_db_user=msfuser --build-arg msf_db_password=msfadmin . -t msfremote`

`docker build . -t msfremote`

### Commands to run
Mounts **host** _/tmp/data_ to container's _/tmp/data_

If no environment variable `TEST_RESOURCE_FILE_LINK` set when run, `TEST_RESOURCE_FILE_LINK` got default value https://raw.githubusercontent.com/TIGER-Framework/tiger_msf_tests/msfdocker/test_resource_file/test.rc

`docker run --name msf --volume=/tmp/data:/tmp/data msfremote`

Set `TEST_RESOURCE_FILE_LINK` when run:

`docker run -e TEST_RESOURCE_FILE_LINK="https://raw.githubusercontent.com/bluscreenofjeff/Metasploit-Resource-Scripts/master/infogather.rc" --volume=/tmp/data:/tmp/data --name msf msfremote`

Creates 4 files inside:
  - msfconsole-test.log
  - test.rc
  - test.rc_results.txt
  - test.rc_errors.txt

#### msfconsole-test.log
Contains verbose log from msfconsole while running

#### test.rc
Contains full code from resource file test (Got by link declared via `TEST_RESOURCE_FILE_LINK`)

#### test.rc_results.txt
Results from executed test by msfconsole

#### test.rc_errors.txt
Any errors from msfconsole
