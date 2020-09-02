你好！
很冒昧用这样的方式来和你沟通，如有打扰请忽略我的提交哈。我是光年实验室（gnlab.com）的HR，在招Golang开发工程师，我们是一个技术型团队，技术氛围非常好。全职和兼职都可以，不过最好是全职，工作地点杭州。
我们公司是做流量增长的，Golang负责开发SAAS平台的应用，我们做的很多应用是全新的，工作非常有挑战也很有意思，是国内很多大厂的顾问。
如果有兴趣的话加我微信：13515810775  ，也可以访问 https://gnlab.com/，联系客服转发给HR。
# bpool [![GoDoc](https://godoc.org/github.com/oxtoacart/bpool?status.png)](https://godoc.org/github.com/oxtoacart/bpool)

Package bpool implements leaky pools of byte arrays and Buffers as bounded channels. 
It is based on the leaky buffer example from the Effective Go documentation: http://golang.org/doc/effective_go.html#leaky_buffer

bpool provides the following pool types:

* [bpool.BufferPool](https://godoc.org/github.com/oxtoacart/bpool#BufferPool)
  which provides a fixed-size pool of
  [bytes.Buffers](http://golang.org/pkg/bytes/#Buffer).
* [bpool.BytePool](https://godoc.org/github.com/oxtoacart/bpool#BytePool) which
  provides a fixed-size pool of `[]byte` slices with a pre-set width (length).
* [bpool.SizedBufferPool](https://godoc.org/github.com/oxtoacart/bpool#SizedBufferPool), 
  which is an alternative to `bpool.BufferPool` that pre-sizes the capacity of
  buffers issued from the pool and discards buffers that have grown too large
  upon return.

A common use case for this package is to use buffers to execute HTML templates
against (via ExecuteTemplate) or encode JSON into (via json.NewEncoder). This
allows you to catch any rendering or marshalling errors prior to writing to a
`http.ResponseWriter`, which helps to avoid writing incomplete or malformed data
to the response.

## Install

`go get github.com/oxtoacart/bpool`

## Documentation

See [godoc.org](http://godoc.org/github.com/oxtoacart/bpool) or use `godoc github.com/oxtoacart/bpool`

## Example

Here's a quick example for using `bpool.BufferPool`. We create a pool of the
desired size, call the `Get()` method to obtain a buffer for use, and call
`Put(buf)` to return the buffer to the pool.

```go

var bufpool *bpool.BufferPool

func main() {

    bufpool = bpool.NewBufferPool(48)

}

func someFunction() error {

     // Get a buffer from the pool
     buf := bufpool.Get()
     ...
     ...
     ...
     // Return the buffer to the pool
     bufpool.Put(buf)

     return nil
}
```

## License

Apache 2.0 Licensed. See the LICENSE file for details.

