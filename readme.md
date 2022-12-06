# Write me a python module that will generate a helm chart for a docker container.

Here is a sample Python module that you can use to generate a Helm chart for a Docker container:

```
import yaml

def generate_chart(image_name, container_port):
  # Create a chart template
  chart = {
    'apiVersion': 'v2',
    'name': 'mychart',
    'version': '0.1.0',
    'description': 'A Helm chart for deploying a Docker container',
    'maintainers': [
      {
        'name': 'Your Name',
        'email': 'your@email.com'
      }
    ],
    'appVersion': '1.0.0',
    'icon': 'https://raw.githubusercontent.com/helm/chartmuseum/master/logo/logo.png',
    'sources': [
      'https://github.com/helm/charts'
    ],
    'home': 'https://github.com/helm/charts',
    'keywords': [
      'container',
      'docker',
      'helm'
    ],
    'engine': 'gotpl',
    'dependencies': [],
    'templates': [
      {
        'name': 'deployment.yaml',
        'data': '''
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  labels:
    app: myapp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: {}
        ports:
        - containerPort: {}
'''.format(image_name, container_port)
      },
      {
        'name': 'service.yaml',
        'data': '''
apiVersion: v1
kind: Service
metadata:
  name: myapp
  labels:
    app: myapp
spec:
  type: LoadBalancer
  ports:
  - port: {}
    protocol: TCP
    targetPort: {}
  selector:
    app: myapp
'''.format(container_port, container_port)
      }
    ],
  }

  # Write chart to a file
  with open('mychart.yaml', 'w') as chart_file:
    yaml.dump(chart, chart_file)
```

# Example usage

`generate_chart('nginx:latest', 80)`

This module defines a generate_chart() function that takes two arguments: the name of the Docker image and the port that the container exposes. It then creates a Helm chart template with a deployment and service manifest that uses the specified image and port. The chart is written to a file called mychart.yaml.
To use this module, you would need to install the PyYAML library, which can be done with the following command:

`pip install pyyaml`

Once you have installed PyYAML, you can use the generate_chart() function like this:

```
import generate_chart

generate_chart('nginx:latest', 80)

```

This will generate a Helm chart file called `mychart.yaml`
