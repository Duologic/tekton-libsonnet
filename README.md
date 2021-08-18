# Tekton jsonnet library

Jsonnet library for https://tekton.dev/

## Usage

Install it with jsonnet-bundler:

```console
jb install https://github.com/Duologic/tekton-libsonnet
```

Import into your jsonnet:

```jsonnet
local tekton = import 'github.com/Duologic/tekton-libsonnet/main.libsonnet';

{
  tekton: tekton.installation,

  git_clone_task: tekton.tasks.task_git_clone,

  pipeline:
    local pipeline = tekton.core.v1beta1.pipeline;
    local workspace = 'ws';

    pipeline.new('tanka-pipeline')
    + pipeline.withWorkspace(workspace)
    + pipeline.addTask(
      'git-clone',
      'git-clone',
      workspaces=[{
        name: 'output',
        workspace: workspace,
      }],
      params=[{
        name: 'url',
        value: 'https://github.com/Duologic/tekton-libsonnet.git',
      }]
    ),
}
```
