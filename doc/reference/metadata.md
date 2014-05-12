# Metadata Fields
NkSIP allows the retrieval of specific information from requests, reponses, dialogs and subscriptions.
The available options are defined here.

* [Requests and Responses](#requests-and-responses-metadata)
* [Dialogs](#fialog-metadata)
* [Subscriptions](#subscriptions-metadata)



## Request and Responses Metadata
Accesible when calling `nksip_request:meta/2`, `nksip_response:meta/2` and when using the option `meta` in the [requests sending functions](../guide/sending_requests.md).

Name|Type|Description
---|---|---
id|`nksip:id()`|Request or response's id
app_id|`nksip:app_id()`|Internal SipApp name this request or response belongs to
app_name|`term()`|User SipApp name this request or response belongs to
dialog_id|`nksip:id()`|Dialog's id of this request or response
subscription_id|`nksip_id()`|Subscription's id of this request or response
proto|`nksip:protocol()`|Transport protocol
local|`{nksip:protocol(),inet:ip_address(),inet:port_number()}`|Local transport protocol, ip and port
remote|`{nksip:protocol(),inet:ip_address(),inet:port_number()}`|Remote transport protocol, ip and port
method|`nksip:method(`)|Method of the request (undefined if it is a response)
ruri|`nksip:uri()`|RUri of the request
scheme|`nksip:scheme()`|Scheme of RUri
user|`binary()`|User of RUri
domain|`binary()`|Domain of RUri
aor|`nksip:aor()`|Address-Of-Record of the RUri
code|`nksip:response_code()`|SIP Code of the response (0 if it as request)
reason_phrase|`binary()`|Reason Phrase of the response
content_type|`nksip:token()`|Content-Type header
body|`nksip:body()`|Body
call_id|`nksip:call_id()`|Call-ID header
vias|`[nksip:via()]`|Via headers
from|`nksip:uri()`|From header
from_tag|`nksip:tag()`|From tag
from_scheme|`nksip:scheme()`|From SIP scheme
from_user|`binary()`|From user
from_domain|`binary()`|From domain
to|`nksip:uri()`|To header
to_tag|`nksip:tag()`|To tag
to_scheme|`nksip:scheme()`|To SIP scheme
to_user|`binary()`|To user
to_domain|`binary()`|To domain
cseq_num|`integer()`|CSeq (numeric part)
cseq_method|`nksip:method()`|CSeq (method part)
forwards|`integer()`|Max-Forwards header
routes|`[nksip:uri()]`|Route headers
contacts|`[nksip:uri()]`|Contact headers
require|`[binary()]`|Tokens in Require header
supported|`[binary()]`|Tokens in Supported header
expires|`integer()`&#124;`undefined`|Expires header
event|`nksip:token()`&#124;`undefined`|Token in Event header
realms|`[binary()]`|Realms in authentication headers
rseq_num|`integer()`&#124;`undefined`|RSeq header (numeric part)
rack|`{integer(),integer(),nksip:method()}`&#124;`undefined`|RAck header
{header, Name}|`[binary()]`|Gets an unparsed header value
all_headers|`[{binary(),[binary()]}]`|Gets all headers and values

Besides this values, you can use any string() or binary() to the get that header's value


## Dialogs Metadata
Available when calling `nksip_dialog:meta/2`.

Name|Type|Description
---|---|---
id|`nksip:id()`|Dialog's Id
app_id|`nksip:app_id()`|Internal SipApp name this dialog belongs to
app_name|`term()`|User SipApp name this dialog belongs to
created|`nksip_lib:timestamp()`|Creation date
updated|`nksip_lib:timestamp()`|Last update
local_seq|`integer()`|Local CSeq number
remote_seq|`integer()`|Remote CSeq number
local_uri|`nksip:uri()`|Local URI
raw_local_uri|`binary()`|Unparsed Local URI
remote_uri|`nksip:uri()`|Remote URI
raw_remote_uri|`binary()`|Unparsed Remote URI
local_target|`nksip:uri()`|Local Target URI
raw_local_target|`binary()`|Unparsed Local Target URI
remote_target|`nksip:uri()`|Remote Target URI
raw_remote_target|`binary()`|Unparsed Remote Target URi
early|`boolean()`|Early dialog (no final response yet)
secure|`boolean()`|Secure (sips) dialog
route_set|`nksip:uri()}`|Route Set
raw_route_set|`binary()`|Unparsed Route Set
invite_status|`nksip_dialog:status()`|Current dialog's INVITE status
invite_answered|`nksip_lib:timestamp()}`|Answer (first 2xx response) timestamp for INVITE usages
invite_local_sdp|`nksip:sdp()}`|Current local SDP
invite_remote_sdp|`nksip:sdp()}`|Current remote SDP
invite_timeout|`integer()`|Seconds to expire current state
invite_session_expires|`integer()`|Seconds to expire current session
invite_refresh|`integer()`|Seconds to refresh
subscriptions|`nksip:id()`|Lists all active subscriptions
call_id|`nksip:call_id()`|Call-ID of the dialog
from_tag|`binary()`|From tag
to_tag|`binary()`|To tag


## Subscriptions Metadata
Available when calling `nksip_subscription:meta/2`.
All dialog options are available for subscriptions, and also:

Name|Type|Description
---|---|---
id|`nksip:id()`|Subscription's Id
status|`nksip_subscription:status()`|Subscription's current status
event|`nksip:token()`|Event header
raw_event|`binary()`|Unparsed Event header
class|`uac`&#124;`uas`|Class of the event, as a UAC or a UAS
answered|`nksip_lib:timestamp()`&#124;`undefined`|Time first NOTIFY was received
expires|`integer()`|Seconds reamaining to subscription expiration