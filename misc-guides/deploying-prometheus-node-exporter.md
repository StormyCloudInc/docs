# Deploying Prometheus Node Exporter

```
# Download Node Exporter
wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-amd64.tar.gz

# Extract the downloaded file
tar xvfz node_exporter*

# Move the binary to /usr/local/bin
sudo mv node_exporter-*/node_exporter /usr/local/bin/

# Create a user for Node Exporter
sudo useradd -rs /bin/false node_exporter

# Create a systemd service file for Node Exporter
sudo bash -c 'cat << EOF > /etc/systemd/system/node_exporter.service
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter --web.listen-address=:9100

[Install]
WantedBy=multi-user.target
EOF'

# Reload systemd to apply the new service
sudo systemctl daemon-reload

# Start the Node Exporter service
sudo systemctl start node_exporter

# Enable the service to start on boot
sudo systemctl enable node_exporter

# Check the status of the Node Exporter service
sudo systemctl status node_exporter
```
