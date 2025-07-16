var url = ""
if OS.has_feature("HTML5"):
	url = "https://godot-python-game.onrender.com/execute_code"
else:
	url = "http://127.0.0.1:8000/execute_code"

var error = http_request.request(url, headers, HTTPClient.METHOD_POST, body)
