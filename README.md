### conda
---
https://github.com/conda/conda/

```py
// tests/core/test_package_cache_data.py

CHANNEL_DIR = abspath(join(dirname(__file__), '..', 'data', 'conda_format_repo'))
CONDA_PKG_REPO = url_path(CHANNEL_DIR)

subdir = "win-64"
zlib_base_fn = "zlib.1.2.11-xxx_3"
zlib_tar_bz2_fn = "zlib.1.2.11-xxx_3"
zlib_tar_bz2_prec = PackageRecord.from_objects({
  "",
  "",
  "",
  "",
  },
  fn=zlib_tar_bz2_fn,
  url="%s/%s/%s" % (CONDA_PKG_REPO, subdir, zlib_tar_bz2_fn),
)
zlib_conda_fn = "zlib-1.2.11-xxx_3.conda"
zlib_conda_prec = PackageRecord.from_objects({
})

def test_ProgressiveFetchExtract_prefers_conda_v2_format():
  with env_var('CONDA_USE_ONLY_TAR_BZ2', False, stack_callback=conda_tests_ctxt_mgmt_def_pol):
    index = get_index([CONDA_PKG_REPO], prepend=False)
    rec = next(iter(index))
    for rec in index:
      if rec.name == 'zlib':
        break
    cache_action, extract_action = ProgressiveFetchExtract.make_actions_for_record(rec)
  assert cache_action.target_package_basename.endswith('.conda')
  assert extract_action.source_full_path.endswith('.conda')

def test_tar_bz2_in_pkg_cache_used_instead_of_conda_pkg():
  with make_temp_package_cache() as pkgs_dir:
    pfe = ProgressiveFetchExtract((zlib_tar_bz2_prec,))
```

```
```

```
```
