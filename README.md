# Logstash grok pattern for Apache

Defined logstash filter pattern for apache log format. 

## How To

- Deploy pattern file to `/etc/logstash/patterns/apache

## Pattern

- apache common access log

```
HTTPD_ACCESSLOG_COMMON (?:%{IPV4:clientip}|-) (?:%{DATA:remote_user}|-) (?:%{DATA:ident}|-) \[%{HTTPDATE:date_timestamp}\] \"(?:%{WORD:method} %{NOTSPACE:request_uri}(?: HTTP/%{NUMBER:httpversion})?|%{DATA:raw_request})\" %{NUMBER:status} (?:%{NUMBER:bytes}|-)
```

- apache combined access log

```
HTTPD_ACCESSLOG_COMBINED (?:%{IPV4:clientip}|-) (?:%{DATA:remote_user}|-) (?:%{DATA:ident}|-) \[%{HTTPDATE:date_timestamp}\] \"(?:%{WORD:method} %{NOTSPACE:request_uri}(?: HTTP/%{NUMBER:httpversion})?|%{DATA:raw_request})\" %{NUMBER:status} (?:%{NUMBER:bytes}|-) \"%{DATA:http_referer}\" \"%{DATA:http_user_agent}\"
```

- apache combined access log with IO

If you need to enable `mod_logio.c` to use `%I` and `%O` then use pattern io_apache

```
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\" %I %O %T "
```

Then pattern

```
HTTPD_ACCESSLOG_IO_COMBINED (?:%{IPV4:clientip}|-) (?:%{DATA:remote_user}|-) (?:%{DATA:ident}|-) \[%{HTTPDATE:date_timestamp}\] \"(?:%{WORD:method} %{NOTSPACE:request_uri}(?: HTTP/%{NUMBER:httpversion})?|%{DATA:raw_request})\" %{NUMBER:status} (?:%{NUMBER:bytes}|-) \"%{DATA:http_referer}\" \"%{DATA:http_user_agent}\" (?:%{NUMBER:request_length}|-) (?:%{NUMBER:body_bytes_sent}|-) (?:%{NUMBER:request_time}|-)
```

