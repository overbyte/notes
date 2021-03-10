# Quick Aliyun OSS Tips

## stopping HTML files downloading

In the details for the file, use the `Set HTTP Headers` and use:

```
Content-Disposition: attachment=filename;
```
