<script>
// Allows stubbing BaseLink in unit tests
const BaseLink = 'BaseLink'

export default {
  // Functional components are stateless, meaning they can't
  // have data, computed properties, etc and they have no
  // `this` context.
  functional: true,
  props: {
    routes: {
      type: Array,
      required: true,
    },
  },
  // Render functions are an alternative to templates
  render(h, { props, $style = {} }) {
    function getRouteTitle(route) {
      return typeof route.title === 'function' ? route.title() : route.title
    }

    // Functional components are the only components allowed
    // to return an array of children, rather than a single
    // root node.
    return props.routes.map((route) => (
      <BaseLink
        tag='li'
        key={route.name}
        to={route}
        exact-active-class={$style.active}
      >
        <a>
          <div class='tile is-parent p-0'>
            <div class='tile is-1 is-child'>
              <span class='p-3 mr-1'>
                <b-icon icon={route.icon}></b-icon>
              </span>
              <span>{getRouteTitle(route)}</span>
            </div>
          </div>
        </a>
      </BaseLink>
    ))
  },
}
</script>

<style lang="scss" module>
@import '@design';
li {
  display: block;
  margin-right: $size-grid-padding;
  margin-right: 0;
  margin-bottom: 0.5em;
  overflow: hidden;
  text-align: left;
  background: lighten($color-body-bg, 10%);
  border-radius: 12px;
  span {
    display: inline-block;
  }
  span:first-child {
    background: lighten($color-body-bg, 30%);
  }
}
</style>
