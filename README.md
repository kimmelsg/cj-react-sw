# react-sw
A top-level React component that lets you interact with a service worker


##API

####Prefetch 


```js
import { Prefetch } from 'react-sw'

const externalAssets [
 'https://image.com'
]

export default () => (
  <div>
    {externalAssets.forEach(url => <Prefetch url={url} /> )}
  </div>
)

class Link extends React.Component {
    render() {
    let { to, children } = this.props
    
    return (
      <Prefetch url={to}>
        <a href={to}>{children}</a>
      </Prefetch>
    )
  }
}

```

####Caching Requests

This service worker will cache all get requests by default. We've added custom stuff so that you can manually cache post requests as well.
Generally, you won't want to do this, but there are cases where your search system may use post over get (such as algolia)

```js
import { CacheRequest } from 'react-sw'

class Request extends React.Component {

  componentDidMount() {
    //load from api
    this.setState({ response })
  }
  
  render() {
    return (
      <div>
        <CacheRequest url="/api/test" value={this.state.response} />
      </div>
    )
  }
}

```
`Cache` will only update the cache if the value exists.


###Cache Assets

```js
import { Cache } from 'react-sw'

export default () => (
  <Cache url="http://google.com/image.png"><img src="http://google.com/image.png"/></Cache>
)
```
