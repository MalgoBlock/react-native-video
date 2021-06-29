# Ad Integration for React Native Video

## Usage

The same as [react-native-video](https://github.com/react-native-community/react-native-video), with the following additions.

### Simple Example
```
import React, {Component} from 'react';
import {StyleSheet, View} from 'react-native';
import Video from '@endemolshinegroup/react-native-video-with-ads';

export default class App extends Component {

  state = {
    paused: false
  }

  constructor(props) {
    super(props);
    this.onAdsLoaded = this.onAdsLoaded.bind(this);
    this.onAdStarted = this.onAdStarted.bind(this);
    this.onAdsComplete = this.onAdsComplete.bind(this);
  }

  componentDidMount() {
    this._video.requestAds("https://pubads.g.doubleclick.net/gampad/ads?sz=640x480&iu=/124319096/external/single_ad_samples&ciu_szs=300x250&impl=s&gdfp_req=1&env=vp&output=vast&unviewed_position_start=1&cust_params=deployment%3Ddevsite%26sample_ct%3Dlinear&correlator=");
  }

  onAdsLoaded() {
    setTimeout(() => {
      this._video.startAds();
    }, 10000);
  }

  onAdStarted() {
    this.setState({paused: true});
  }

  onAdsComplete() {
    this.setState({paused: false});
  }

  render() {
    return (
      <View style={styles.container}>
        <Video
            ref={component => this._video = component}
            source={{uri: "http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"}}
            style={{width: 300, height: 300}}
            paused={this.state.paused}
            onAdsLoaded={this.onAdsLoaded}
            onAdStarted={this.onAdStarted}
            onAdsComplete={this.onAdsComplete}
          >
          </Video>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  }
});
```

### Event props

#### onAdError
Callback function that is called when there is an error while loading an ad. When an error occurs the video will continue playback automatically. If you require additional functionality, use this callback

Payload: none

Platforms: Android ExoPlayer, iOS

#### onAdsComplete
Callback function that is called when all loaded ads have finished playing. This callback should be used to re-start your Video.

Payload: none

Platforms: Android ExoPlayer, iOS

#### onAdsLoaded
Callback function that is called when Ads have been loaded.
Payload: none

Platforms: Android ExoPlayer, iOS

#### onAdStarted
Callback function that is called when Ads have started to play. This should be used to pause your Video.

Payload: none

Platforms: Android ExoPlayer, iOS

### Methods
Methods operate on a ref to the Video element. You can create a ref using code like:
```
return (
  <Video source={...}
    ref => (this.player = ref) />
);
```

#### requestAds

Request ads from the give url

Example:
```
let url = "https://pubads.g.doubleclick.net/gampad/ads?sz=640x480&iu=/124319096/external/single_ad_samples&ciu_szs=300x250&impl=s&gdfp_req=1&env=vp&output=vast&unviewed_position_start=1&cust_params=deployment%3Ddevsite%26sample_ct%3Dlinear&correlator="
this.player.requestAds(url);
```

Platforms: Android ExoPlayer, iOS

#### startAds

Request that the loaded ads start playing

Example:
```
this.player.startAds();
```

Platforms: Android ExoPlayer, iOS


**MIT Licensed**