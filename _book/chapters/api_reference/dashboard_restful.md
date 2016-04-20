# Dashboard RESTful API

> This document has to improve a lot, in the meanwhile, check how the frontend makes
use of it.

### public/components/apps/app.jsx
```javascript
launch () {
    const { name } = this.props

    request.post('/api/activities/' + name).then(() => {
      return request.get('/i/' + name).promise()
    }).then(() => {
      this.router.push('/i/' + name)
    }).catch((err) => {
      if (err.status === 404) return toastr.info(`${name} is running`)
      toastr.error(err.message)
    })
  }

  install () {
    const url = this.props.git_url

    request.post('/api/apps').send({ url }).then((res) => {
      const name = res.body.name
      const props = res.body.netbeast
      const type = props ? props.type : 'app'

      toastr.success(`${name} has been installed!`)

      if (type === 'plugin' || type === 'service' || props.bootOnLoad)
        return request.post('/api/activities/' + name).promise()
    }).then((res) => { toastr.success(`${res.body.name} is running`) })
    .catch((fail, res) => toastr.error(res.text))
  }

  stop () {
    const { name } = this.props
    request.del('/api/activities/' + name).end((err, res) => {
      if (err) return toastr.error(res.text)
      this.setState({ hidden: true })
      toastr.info(name + ' has been stopped.')
    })
  }

  uninstall () {
    const { name } = this.props
    request.del('/api/apps/' + name).end((err, res) => {
      if (err) return toastr.error(res.text)
      this.setState({ hidden: true })
      toastr.info(name + ' has been removed.')
    })
  }
```

### public/components/apps/drawer.jsx
_**query** can be modules, apps, activities or plugins_
```javascript
loadApps (props, done) {
  const { route } = props
  const pathname = route.path ? route.path : 'apps'
  const query = pathname === 'uninstall' ? 'modules' : pathname

  request.get(`/api/${query}/`).end((err, res) => {
    if (err) return toastr.error(err)

    let apps = [ ...res.body ] // smart copy
    apps.forEach((app) => app.type = pathname)

    Session.save('apps', apps)
    this.setState({ apps: apps, pathname: pathname })
  })
}
```
