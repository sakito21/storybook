# Storybook Docs Recipes

[Storybook Docs](../README.md) consists of two basic mechanisms, [DocsPage](docspage.md) and [MDX](mdx.md). But how should you use them in your project?

- [Component Story Format (CSF) with DocsPage](#component-story-format-csf-with-docspage)
- [Pure MDX Stories](#pure-mdx-stories)
- [Mixed CSF / MDX Stories](#mixed-csf--mdx-stories)
- [CSF Stories with MDX Docs](#csf-stories-with-mdx-docs)
- [More resources](#more-resources)

## Component Story Format (CSF) with DocsPage

Storybook's [Component Story Format (CSF)](https://medium.com/storybookjs/component-story-format-66f4c32366df) is a convenient, portable way to write stories. [DocsPage](docspage.md) is a convenient, zero-config way to get rich docs for CSF stories. Using these together is a primary use case for Storybook Docs.

If you want to intersperse longform documentation in your Storybook, for example to include an introductory page at the beginning of your storybook with an explanation of your design system and installation instructions, [Documentation-only MDX](mdx.md#documentation-only-mdx) is a good way to achieve this.

## Pure MDX Stories

[MDX](mdx.md) is an alternative to syntax to CSF that allows you co-locate your stories and your documentation. Everything you can do in CSF, you can do in MDX. And if you're consuming it in [Webpack](https://webpack.js.org/), it exposes an _identical_ interface, so the two files are interchangeable. Some teams will choose to write all of their Storybook in MDX and never look back.

## Mixed CSF / MDX Stories

Can't decide between CSF and MDX? In transition? Or have did you find that each format has its own use? There's nothing stopping you from keeping some of your stories in CSF and some in MDX. And if you want to migrate one way or another, the [csf-to-mdx and mdx-to-csf codemod migrations](https://github.com/storybookjs/storybook/blob/next/lib/codemod/README.md) make it easy.

The only limitation is that your exported titles (CSF: `default.title`, MDX `Meta.title`) should be unique across files. Loading will fail if there are duplicate titles.

## CSF Stories with MDX Docs

Perhaps you want to write your stories in CSF, but document them in MDX? Here's how to do that:

**Button.stories.mdx**

```md
import { Story } from '@storybook/docs/blocks';
import { SomeComponent } from 'somewhere';

# Button

I can embed a story (but not define one, since this file should not contain a `Meta`):

<Story id="some--id">

And of course I can also embed arbitrary markdown & JSX in this file.

<SomeComponent prop1="val1" />
```

**Button.stories.js**

```js
import { Button } from './Button';
import mdx from './Button.stories.mdx';

export default {
  title: 'Demo/Button',
  parameters: {
    docs: mdx.parameters.docs,
  },
};

export const basic = () => <Button>Basic</Button>;
```

## More resources

Want to learn more? Here are some more articles on Storybook Docs:

- References: [README](../README.md) / [DocsPage](docspage.md) / [MDX](mdx.md) / [FAQ](faq.md)
- Vision: [Storybook Docs sneak peak](https://medium.com/storybookjs/storybook-docs-sneak-peak-5be78445094a)
- [Technical preview guide](https://docs.google.com/document/d/1un6YX7xDKEKl5-MVb-egnOYN8dynb5Hf7mq0hipk8JE/edit?usp=sharing)
