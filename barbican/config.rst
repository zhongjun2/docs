 curl -g -i -X GET http://127.0.0.1/key-manager/v1/secrets/a6db0d6a-43fc-45a3-ac6f-9dae79f3b0dc -H "Accept: application/json" -H "User-Agent: osc-lib/1.10.0 keystoneauth1/3.5.0 python-requests/2.18.4 CPython/2.7.12" -H "X-Auth-Token: gAAAAABa3to-s2nXhwRVwGge8z0DPh00wbApJrwO7vuH50kS6SdVYzLWEQ2EOESh0wBczeyliRk_DJBv-m3XyjNtbXVA2yqyuYpUIIDUc_RJt5bs68GsxKBxAdFVnKIXKV85GqZXYI6F5NJ9aCL0Y_6hTsgBkZcV03wcKYsacAd70EizPvgYvto"
 
 
 
  curl -g -i -X GET http://127.0.0.1/key-manager/v1/secret-stores -H "Accept: application/json" -H "User-Agent: osc-lib/1.10.0 keystoneauth1/3.5.0 python-requests/2.18.4 CPython/2.7.12" -H "X-Auth-Token: gAAAAABa3uBWg7lfr13RUiTadkwk1hmRrHgscYXIaihKi3Xlzk2Pq1YTg_j8UYYxxWOatXTD_6IYu2nfWISYbR_qd3Y08kLDeSdshlx1pC33940ueBUkgLiRp1pN8KMNiImzjl311OkUkn793cZ0b9pZ1m0Frs1gLhFfGUnDQ5We6fxfoS7CEZg"
  
  
    curl -g -i -X GET http://127.0.0.1/key-manager/v1/secret-stores/global-default -H "Accept: application/json" -H "User-Agent: osc-lib/1.10.0 keystoneauth1/3.5.0 python-requests/2.18.4 CPython/2.7.12" -H "X-Auth-Token: gAAAAABa3uBWg7lfr13RUiTadkwk1hmRrHgscYXIaihKi3Xlzk2Pq1YTg_j8UYYxxWOatXTD_6IYu2nfWISYbR_qd3Y08kLDeSdshlx1pC33940ueBUkgLiRp1pN8KMNiImzjl311OkUkn793cZ0b9pZ1m0Frs1gLhFfGUnDQ5We6fxfoS7CEZg"

  
[secretstore]
# Set to True when multiple plugin backends support is needed
enable_multiple_secret_stores = True
stores_lookup_suffix = software, kmip, pkcs11, dogtag

[secretstore:software]
secret_store_plugin = store_crypto
crypto_plugin = simple_crypto

[secretstore:kmip]
secret_store_plugin = kmip_plugin
global_default = True

[secretstore:dogtag]
secret_store_plugin = dogtag_plugin

[secretstore:pkcs11]
secret_store_plugin = store_crypto
crypto_plugin = p11_crypto


curl -g -i -X DELETE http://127.0.0.1/volume/v3/9daf2979524646b1951c985a3236d661/volumes/4ef8a6de-43ac-40b3-b26f-20afc09989f6/metadata/aaa.bbb.....ccc88 -H "Accept: application/json" -H "X-Openstack-Cinder-Api-Version: 1.0" -H "User-Agent: python-cinderclient" -H "X-Auth-Token: gAAAAABa4Fu313p4nkuV8s0EjXUcfsskmN8kr_LY8-l9rDr6m8tHTjbyyypaLTu7_RsKmAIl42rc34rH1hn2o5_npVzLqSU9oqxtw8CYBxTAdrZ5DLoHrZLghwGG1KKKPABCx7WxVyXAK_RXyTItinQ5RJkYYHGZ-GSNYW_oPKOfNbX6kVshhpk" -H "X-OpenStack-Request-ID: req-87f09c88-ff7e-4b3b-8015-99424981a19d"


 curl -i -X DELETE http://127.0.0.1:8786/v2/9daf2979524646b1951c985a3236d661/shares/3c423bdc-609d-4adf-9cd5-0fb4faa79130/metadata/aaa.bbb.ccc...jkdf -H "X-Openstack-Manila-Api-Version: 2.4" -H "X-Auth-Token: gAAAAABa4F2o7b25Z4MUzKWa5k9HofUHJ0WNIc0qpLtLMOYC7nODV5A7oPawHPa-c1pzvKSjO24v9xXbiC1v2-n4WAblrq409k8jN2C_kuQlJwwsm0-g0gjA7fWN3phJxvSKOuLuRIGk_nF0CDLq-WNwkpwwBOYf9IbEBv91-26gYV6NNMZaLjg" -H "Accept: application/json" -H "User-Agent: python-manilaclient"
 
enabled_secretstore_plugins = kmip_crypto

[kmip_plugin]
username = 'admin'
password = 'password'
host = localhost
port = 5696
keyfile = '/path/to/certs/cert.key'
certfile = '/path/to/certs/cert.crt'
ca_certs = '/path/to/certs/LocalCA.crt'


https://github.com/OpenKMIP/PyKMIP/wiki/Configuration#server-configuration

[server]
hostname=127.0.0.1
port=5696
certificate_path=/etc/pykmip/certs/pykmip-server-cert.pem
key_path=/etc/pykmip/certs/pykmip-server-key.pem
ca_path=/etc/pykmip/certs/pykmip-server-cert.pem
auth_suite=Basic
policy_path=/etc/pykmip/policies
enable_tls_client_auth=True
tls_cipher_suites=
    TLS_RSA_WITH_AES_128_CBC_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
logging_level=DEBUG


[client]
host=127.0.0.1
port=5696
keyfile=/etc/pykmip/certs/client_private_key.pem
certfile=/etc/pykmip/certs/client_cert.pem
cert_reqs=CERT_REQUIRED
ssl_version=PROTOCOL_SSLv23
ca_certs=/etc/pykmip/certs/pykmip-server-cert.pem
do_handshake_on_connect=True
suppress_ragged_eofs=True
username=
password=



生成证书
.

openssl req -x509 -newkey rsa:2048 -keyout /etc/keystone/keystone-saml-key.pem -out /etc/keystone/keystone-saml-cert.pem -days 9999 -nodes

openssl req -x509 -newkey rsa:2048 -keyout /etc/pykmip/certs/pykmip-server-key.pem -out /etc/pykmip/certs/pykmip-server-cert.pem -days 9999 -nodes


openssl req -x509 -newkey rsa:2048 -keyout /etc/pykmip/certs/client_private_key.pem -out /etc/pykmip/certs/client_cert.pem -days 9999 -nodes
