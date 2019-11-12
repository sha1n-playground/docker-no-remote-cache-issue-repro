# Docker Images Remote Cache Control Issue Reproduction
This repository reproduces an issue in which the flag `--experimental_allow_tags_propagation` apparently doesn't 
propagate the `no-cache` / `no-remote-cache` to actions used by the `container_image` rule.  
I first reported this issue [here](https://github.com/bazelbuild/rules_docker/issues/764#issuecomment-552329419).


I used the following command, followed by `bazel clean` several times to reproduce the issue and created a chrome 
tracing profile (see: profile.json.gz) in which remote-cache activity can be observed clearly. 
```bash
bazel build //... --remote_cache=http://localhost:8080/cache --experimental_allow_tags_propagation --profile=profile.json.gz --experimental_generate_json_trace_profile
```

This issue reproduces on Bazel 1.0.0, 1.0.1 and 1.1.0.
