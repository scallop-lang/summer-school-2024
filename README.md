# Scallop Summer School (Salem, MA 2024)

## Setup
To run the docker container (build takes around ~20 min):
```
docker build -t scallop-summer24-tutorial -f x86_64/Dockerfile .
docker run -it --name scallop-summer scallop-summer24-tutorial
```
For running the container on a non-x86 machine, consider using the [--platform](https://docs.docker.com/build/building/multi-platform/) flag.

After this, you should see the following prompt:
```
(base) root@c36cbd85bb7b:~/labs$
```
Be sure to activate the conda environment with:
```
conda activate scallop-env
```
To use OpenAI features, add the following line to the container's `~/.bashrc`:
```bash
export OPENAI_API_KEY="<YOUR_OPENAI_KEY>"
```

## Tutorial instructions
See the [official website](https://www.scallop-lang.org/ssnp24/index.html).

## Solutions
See the `solutions` branch.