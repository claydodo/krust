# LS

## `LS`, `LS_R`

### `LS(root=None, pattern=None, with_root=None, ignore_hidden=True, use_glob=None)`

#### behavior

* `root` is always expanded by `P` before use.
* `*`, `?`, etc in `root` are always treated as glob wildcards, not regex.
* when glob wildcards exists in `root` and `use_glob` is not explicitly set to `False`, the result contains root dir part (even if `with_root=True`); else base part only.
    * unlike shell `ls`, sub dirs are not listed further.
* if `with_root` is explicitly set to `True/False`, root dir parts are turned on/off by force (except when root is glob, this parameter has no effect and root part is always on); but if `root` is None, there will be no root dir parts anyway. 


```python
>>> LS() 
['a.txt', 'b', ...]  # base only

>>> LS('.')
['a.txt', 'b', ...]  # base only

>>> LS('.', with_root=True)
['./a.txt', './b', ...]  # with root part

>>> LS('some_dir')
['1.nc', '2.nc', 'sub_dir', ...]  # base only

>>> LS('some_dir/*')
['some_dir/1.nc', 'some_dir/2.nc', 'some_dir/sub_dir', ...]  # with root part. sub dirs are not listed further.

>>> LS('some_dir/*', with_root=False)
['some_dir/1.nc', 'some_dir/2.nc', 'some_dir/sub_dir', ...]  # when root is glob, with_root has no effect.

```

* `pattern` is applied to result's full path if it contains `/`, else to base name only.


### `LS_R(root=None, pattern=None, with_root=None, ignore_hidden=True, glob=None)`

* recursive version of `LS`.
