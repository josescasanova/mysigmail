<template>
  <div>
    <table
      style="font-family: Arial, Helvetica, sans-serif; line-height: 1.5"
      :style="{
        fontSize: options.font.size + 'px',
        fontFamily: options.font.family
      }"
    >
      <tbody>
        <tr>
          <td style="vertical-align: top;">
            <img
              v-if="image"
              :src="image"
              :style="{
                'width': options.avatar.size + 'px',
                'height': options.avatar.size + 'px',
                'border-radius': options.avatar.roundness + 'px',
                'margin-right': '10px',
              }"
            >
            <div
              v-else
              style="margin-right: 10px; background: #eee;"
              :style="{
            'height': options.avatar.size + 'px',
            'width': options.avatar.size + 'px',
            'border-radius': options.avatar.roundness + 'px'
          }"
            ></div>
          </td>
          <td style="vertical-align: top;">
            <span style="display: block;" :style="{fontSize: `${options.font.size + 2}px` }">
              <span
                style="font-weight: 600"
                :style="{color: options.color.mainPreview || options.color.main}"
              >{{ mainFields[0].value }}</span>
            </span>
            <span style="display: block; margin-bottom: 10px;">
              <span>{{ mainFields[1].value }}</span>
              <span v-if="mainFields[2].value">
                <span v-if="options.separator !== 'br'">&nbsp;{{ options.separator }}&nbsp;</span>
                <br v-else>
              </span>
              <span>{{ mainFields[2].value }}</span>
            </span>
            <template v-for="item in otherFields">
              <span v-if="item.value" style="display: block;" :key="item.id">
                <span
                  style="font-weight: 600;"
                  :style="{color: options.color.secondaryPreview || options.color.secondary}"
                >{{ item.name }}:</span>
                <a
                  v-if="item.type === 'link'"
                  :href="formatLink(item.value)"
                  style="text-decoration: none; color: inherit; padding-left: 5px;"
                >{{ item.value }}</a>
                <a
                  v-if="item.type === 'email'"
                  :href="`mailto:${item.value}`"
                  style="text-decoration: none; color: inherit; padding-left: 5px;"
                >{{ item.value }}</a>
                <span v-if="item.type === 'text'" style="padding-left: 5px;">{{ item.value }}</span>
              </span>
            </template>
            <a
              style="display: inline-block; font-size: 0;"
              v-for="item in socials.installed"
              :key="item.name"
              :href="formatLink(item.link)"
            >
              <span
                style="width: 20px; height:20px; display: inline-block; padding: 4px; border-radius: 3px; box-sizing: border-box; margin: 10px 3px 0 0;"
                :style="{
                  backgroundColor: options.color.mainPreview || options.color.main,
                  backgroundImage: `url(https://s3.eu-central-1.amazonaws.com/mysigmail/icons/${item.icon}.png)`,
                  backgroundSize: '12px',
                  backgroundPosition: 'center center',
                  backgroundRepeat: 'no-repeat'
                }"
              ></span>
            </a>
          </td>
        </tr>
      </tbody>
    </table>
    <table
      v-if="isAdded('disclaimer')"
      :style="{
        fontSize: options.font.size + 'px',
        fontFamily: options.font.family,
        color: '#888',
        marginTop: '10px'
      }"
    >
      <tbody>
        <tr>
          <td>
            <span>{{ addons.disclaimer }}</span>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import EmailTemplate from './emailTemplate'

export default {
  extends: EmailTemplate
}
</script>
