<template>
  <transition name="slide">
    <music-list :title="title" :bg-image="bgImage" :songs="songs" :rank="true"></music-list>
  </transition>
</template>

<script type="text/ecmascript-6">
  import MusicList from '@/components/music-list/music-list'
  import {mapMutations, mapGetters} from 'vuex'
  import {getMusicList} from '@/api/rank'
  import {ERR_OK} from '@/api/config'
  import {createSong} from '@/common/js/song'

  export default {
    data () {
      return {
        songs: []
      }
    },
    created () {
      this._getMusicList()
    },
    computed: {
      title () {
        return this.topList.topTitle
      },
      bgImage () {
        return this.topList.picUrl
      },
      ...mapGetters([
        'topList'
      ])
    },
    methods: {
      _getMusicList () {
        getMusicList(this.topList.id).then((res) => {
          if (res.code === ERR_OK) {
            this.songs = this._normalizeSongs(res.songlist)
          }
        })
      },
      _normalizeSongs (list) {
        let ret = []
        list.forEach((item) => {
          const musicData = item.data
          if (musicData.songid && musicData.albumid) {
            ret.push(createSong(musicData))
          }
        })
        return ret
      },
      ...mapMutations({
        setTopList: 'SET_TOPLIST'
      })
    },
    components: {
      MusicList
    }
  }
</script>

<style lang="stylus" scoped ref="stylesheet/stylus">
  .slide-enter-active, .slide-leave-active
    transition: all .4s ease
  .slide-enter, .slide-leave-to
    transform: translate3d(100% 0, 0)
</style>
