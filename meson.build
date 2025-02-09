project(
  'toolbox',
  'c',
  version: '0.0.99.2',
  license: 'ASL 2.0',
  meson_version: '>= 0.53.0',
)

cc = meson.get_compiler('c')

go = find_program('go')
go_md2man = find_program('go-md2man')
patchelf = find_program('patchelf')
shellcheck = find_program('shellcheck', required: false)
skopeo = find_program('skopeo', required: false)

bash_completion = dependency('bash-completion', required: false)

profiledir = get_option('profile_dir')

tmpfilesdir = get_option('tmpfiles_dir')
if tmpfilesdir == ''
  systemd_dep = dependency('systemd')
  tmpfilesdir = systemd_dep.get_pkgconfig_variable('tmpfilesdir')
endif

if bash_completion.found()
  install_data(
    'completion/bash/toolbox',
    install_dir: bash_completion.get_pkgconfig_variable('completionsdir')
  )
endif

if not skopeo.found()
    message('Running system tests requires Skopeo for OCI image manipulation.')
endif

install_subdir(
  'test',
  install_dir: join_paths(get_option('datadir'), meson.project_name()),
  exclude_files: [
    'system/libs/bats-assert/.git',
    'system/libs/bats-assert/.gitignore',
    'system/libs/bats-assert/.travis.yml',
    'system/libs/bats-assert/package.json',
    'system/libs/bats-support/.git',
    'system/libs/bats-support/.gitignore',
    'system/libs/bats-support/.travis.yml',
    'system/libs/bats-support/package.json'
    ],
  exclude_directories: [
    'system/libs/bats-assert/.git',
    'system/libs/bats-assert/script',
    'system/libs/bats-assert/test',
    'system/libs/bats-support/.git',
    'system/libs/bats-support/script',
    'system/libs/bats-support/test'
  ]
)

subdir('data')
subdir('doc')
subdir('profile.d')
subdir('src')
