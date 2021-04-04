# ESP32 Wi-Fi Penetration Tool
## Webserver component

This component provides an UI for user to interact with the tool itself.

It is build on top of `esp_http_server` component that is described on official [ESP-IDF reference page](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/protocols/esp_http_server.html).

HTML sites are stored in RAM and are defined as a constant char array in `pages/`. Currently only one page is provided and it's updated dynamically usign AJAX calls from JavaScript client.
Currently the Webserver is started by calling `webserver_run()` which registers all available endpoints and runs until ESP32 shuts down.

### Endpoints
This webserver implements few enpoints that are used by JavaScript client.
- **`/`** displayes index.html page
- **`/status`** returns attack status in binary
- **`/reset`** tells the application to reset attack status to default READY state
- **`/ap-list`** scans near APs and displays them to table
- **`/run-attack`** sends configuration back to the application
- **`/capture.pcap`** provides PCAP formatted file for download
- **`/capture.hccapx`** provides HCCAPX formatted file for download

### JavaScript client
Endpoints are called using AJAX calls from JavaScript provided on `index.html` page. It also parser reponses from webserver from binary to human readble form.
It should do all additional computations that doesn't neccesarry have to happen on ESP32 to minimize its power consumption. 

## Utils
To make development of web client a bit easier, there is a script `utils/convert_html_to_header_file.sh` available that converts standard HTML file into header file and formats it to make it compilable.

## Reference
Doxygen API reference available