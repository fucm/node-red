<p align=center>
    <img src="https://www.stiebel-eltron.de/apps/ste/docroot/images/single/logo-stiebel-eltron.png"/>
</p>

# Scrapping an ISG Web with node-red
This respository contains the required Node-RED flows to scrape the web interface of a STIEBEL ELTRON Internet-Service Gateway (ISG WEB) and forward the data via MQTT to HA (and optionally to an InfluxDB).

For questions and other inquiries, use the issue tracker in this repo.

# History
After I extended my home installation with a photovoltaic converter of SMA and connected the installations (Stiebel Eltron LWZ504e and SMA Sunny Manager), Modbus was not working anymore on the ISG web and I could scrap my old scrapping method ([python-stiebe-eltron](https://github.com/fucm/python-stiebel-eltron)). The Modbus and EMI “modules” can not run in parallel on the ISG web. The complete history of the marriage between Stiebel Eltron and Home Assistant can be found in this thread, including different solutions: [Is there any interest in a Stiebel Eltron climate platform?](https://community.home-assistant.io/t/is-there-any-interest-in-a-stiebel-eltron-climate-platform/65628)

## Requirements
At minimum you need the following components:
* STIEBEL ELTRON Internet-Service Gateway [ISG WEB](https://www.stiebel-eltron.com/en/home/products-solutions/renewables/controller_energymanagement/internet_servicegateway/isg_web.html)
* STIEBEL ELTRON heatpump (compatible). Successfully used devices:
  * LWZ504e
* [Node-RED](https://nodered.org/), either installed as part of [Home Assistant OS](https://www.home-assistant.io/hassio/installation/) as an Add-on, as a separated docker container or as any other possible deployment option.
* [MQTT Broker](https://mosquitto.org/), either installed as part of [Home Assistant OS](https://www.home-assistant.io/hassio/installation/) as an Add-on, as a separated docker container or as any other possible deployment option.
* Network connection bewteen all components

The setup can easily be extend with the following components to get very nice history graphs.
* [InfluxDB](https://www.influxdata.com/)
* [Grafana](https://grafana.com/)

## Installation

 1. Setup Home Assistant (HA)
 2. Setup the MQTT Brocker
	 1. Add MQTT integration to HA
	 2. Make sure HA is able to receive MQTT messages
 3. Setup Node-RED
	 1. Import the two flows in this repo into Node-RED
	 2. Without InfluxDB: delete the nodes which prepare and send the data to InfluxDB. You don't need them.
	 3. Update the node: "HA MQTT Set device details" with your installation details.
	 4. Verify or add the MQTT broker configuration
	 5. Deploy the flows
 4. Check HA for new sensors

## License
The content of this ``node-red`` repository is licensed under MIT, for more details check LICENSE.