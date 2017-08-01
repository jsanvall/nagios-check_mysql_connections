#!/bin/bash

function usage {
  echo "$(basename $0) usage: "
  echo "    -w warning_level Example: 80"
  echo "    -c critical_level Example: 90"
  echo "    -u username Example: root"
  echo "    -p password Example: 1234"
  echo "    -h host Example: localhost"
  echo "    --defaults-file <FILE_PATH> "
  echo ""
  exit 1
}

while [[ $# -gt 1 ]]
do
  key="$1"
  case $key in
    -w)
    WARN="$2"
    shift
    ;;
    -c)
    CRIT="$2"
    shift
    ;;
    -u)
    USER="$2"
    shift
    ;;
    -p)
    PASS="$2"
    shift
    ;;
    -h)
    HOST="$2"
    shift
    ;;
    --defaults-file)
    FILE="$2"
    shift
    ;;
    *)
    usage
    shift
    ;;
  esac
  shift
done

[ ! -z ${WARN} ] && [ ! -z ${CRIT} ] || usage
if [ ! -z ${FILE} ]; then
  CONNECTIONS=$(echo "show processlist;" | mysql --defaults-file=${FILE} 2> /dev/null | sed 1,1d  | wc -l)
else
  CONNECTIONS=$(echo "show processlist;" | mysql -h ${HOST} -u${USER} -p${PASS}  2> /dev/null | sed 1,1d | wc -l)
fi
if [[ ${CONNECTIONS} -gt ${CRIT} ]]
then
  echo "CRITICAL - ${CONNECTIONS} Database Connections |Connections=${CONNECTIONS};;;;"
  exit 2
elif [[ ${CONNECTIONS} -gt ${WARN} ]]
then
  echo "WARNING - ${CONNECTIONS} Database Connections |Connections=${CONNECTIONS};;;;"
  exit 1
else
  echo "OK - ${CONNECTIONS} Database Connections |Connections=${CONNECTIONS};;;;"
  exit 0
fi
