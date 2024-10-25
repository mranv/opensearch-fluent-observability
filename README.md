# OpenSearch Fluent Observability

A complete logging and observability stack using OpenSearch, Data Prepper, and Fluent Bit for processing and analyzing Nginx logs in real-time.

## 🔍 Overview

This project provides a production-ready logging infrastructure that includes:

- Multi-node OpenSearch cluster for scalable log storage
- OpenSearch Dashboards for log visualization and analysis
- Data Prepper for log transformation and enrichment
- Fluent Bit for efficient log collection
- Pre-configured Nginx log parsing and structuring

## 🏗️ Architecture

```
Nginx Logs → Fluent Bit → Data Prepper → OpenSearch → OpenSearch Dashboards
(Source)     (Collector)  (Transformer)   (Storage)    (Visualization)
```

## 🚀 Quick Start

### Prerequisites

- Docker Engine 20.10.0+
- Docker Compose v2.0.0+
- At least 4GB of available RAM
- Nginx installed on the host machine

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/opensearch-fluent-observability.git
cd opensearch-fluent-observability
```

2. Create required directories:
```bash
mkdir -p config
```

3. Copy configuration files:
```bash
cp config-examples/data-prepper.yaml config/
cp config-examples/fluent-bit.conf config/
```

4. Start the stack:
```bash
docker-compose up -d
```

### Verification

1. Check the OpenSearch cluster health:
```bash
curl http://localhost:9200/_cluster/health
```

2. Access OpenSearch Dashboards:
   - URL: http://localhost:5601
   - Default credentials:
     - Username: admin
     - Password: Anubhav@321

## 📁 Project Structure

```
├── docker-compose.yml          # Main compose file for all services
├── config/
│   ├── data-prepper.yaml      # Data Prepper pipeline configuration
│   └── fluent-bit.conf        # Fluent Bit configuration
├── config-examples/           # Example configurations
└── README.md
```

## 🔧 Configuration

### OpenSearch Configuration
- 2-node cluster setup
- Security plugin disabled for development
- 512MB heap size per node
- Persistent volume storage

### Data Prepper Pipeline
- HTTP source on port 2021
- Grok processor for Nginx log parsing
- Daily index rotation
- Bulk processing with retry logic

### Fluent Bit Settings
- Tail input plugin for Nginx logs
- Custom parser for Nginx log format
- Gzip compression
- Automatic retry mechanism

## 📊 Log Structure

Processed logs include:
- Client IP
- Timestamp
- HTTP Method
- URL
- Response Code
- User Agent
- Additional metadata (hostname, environment)

## 🛠️ Maintenance

### Backup

Backup the OpenSearch data volumes:
```bash
docker run --rm -v opensearch-data1:/data -v $(pwd):/backup alpine tar czf /backup/opensearch-data1.tar.gz /data
```

### Scaling

To add more OpenSearch nodes:
1. Copy the node configuration in docker-compose.yml
2. Update the discovery.seed_hosts
3. Add the new node to OPENSEARCH_HOSTS in dashboard configuration

## 🔐 Security

Default security measures:
- Basic authentication enabled
- SSL/TLS disabled for development (enable for production)
- Default admin password configured

## 🐛 Troubleshooting

Common issues and solutions:

1. OpenSearch fails to start:
   - Check ulimit settings
   - Verify memory settings
   - Review logs: `docker-compose logs opensearch-node1`

2. No logs appearing:
   - Verify Nginx is generating logs
   - Check Fluent Bit configuration
   - Review Data Prepper pipeline status

## 📝 License

MIT License - see LICENSE file for details.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📚 Additional Resources

- [OpenSearch Documentation](https://opensearch.org/docs/latest/)
- [Data Prepper Documentation](https://opensearch.org/docs/latest/data-prepper/index/)
- [Fluent Bit Documentation](https://docs.fluentbit.io/)

## ✨ Acknowledgments

- OpenSearch Project contributors
- Fluent Bit maintainers
- Data Prepper team

---
Created and maintained by [@mranv]# opensearch-fluent-observability
