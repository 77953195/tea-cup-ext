INSTALL

// use yarn
yarn add vue-composition-test-utils -D
// use npm
npm install vue-composition-test-utils -D

DEMO CODE 

import { ref } from 'vue'

export function useCounter(initialValue = 0) {
  const count = ref(initialValue)
  const inc = (delta = 1) => (count.value += delta)
  return { count, inc }
}

RUN 

import { mountComposition, nextTick } from 'vue-composition-test-utils'

test('should get current composition result', function() {
  const wrapper = mountComposition(useCounter)
  expect(wrapper.result.current.count.value).toEqual(0)
});

test('should render template though template option', async function() {
  const wrapper = mountComposition(useCounter, {
    component: {
      template: 'hello world {{result.current.count.value}}',
    }
  })
  expect(wrapper.html()).toEqual('hello world 0')
  await nextTick(() => {
    wrapper.result.current.inc()
  })
  expect(wrapper.result.current.count.value).toEqual(1)
  expect(wrapper.html()).toEqual('hello world 1')
});

API

import {GlobalMountOptions} from "@vue/test-utils/dist/types";
import {ComponentOptionsWithoutProps} from "vue";

interface MountingOptions<Props, Data = {}> {
    data?: () => {} extends Data ? any : Data extends object ? Partial<Data> : any;
    props?: Props;
    attrs?: Record<string, unknown>;
    slots?: SlotDictionary & {
        default?: Slot;
    };
    global?: GlobalMountOptions;
    attachTo?: HTMLElement | string;
    shallow?: boolean;
    component?: ComponentOptionsWithoutProps;
}

interface MountingResult<R> {
    current: R | null;
    error: Error | null;
}

export declare const mountComposition: <R, Props>(callback: () => R, options?: MountingOptions<never>) => import("@vue/test-utils").VueWrapper<import("vue").ComponentPublicInstance<Props, {}, {}, {}, {}, Record<string, any>, import("vue").VNodeProps & Props, {}, false, import("vue").ComponentOptionsBase<any, any, any, any, any, any, any, any, any, {}>>> & {
    result: MountingResult<R>;
};

export const nextTick: (fn?: () => void) => Promise<void>

<table>
    <tr>
        <td><img src="https://oscimg.oschina.net/oscnet/up-3ea20e447ac621a161e395fb53ccc683d84.png"/></td>
        <td><img src="https://oscimg.oschina.net/oscnet/up-a6f23cf9a371a30165e135eff6d9ae89a9d.png"/></td>
		<td><img src="https://oscimg.oschina.net/oscnet/up-ff5f62016bf6624c1ff27eee57499dccd44.png"/></td>
    </tr>
	<tr>
        <td><img src="https://oscimg.oschina.net/oscnet/up-b9a582fdb26ec69d407fabd044d2c8494df.png"/></td>
        <td><img src="https://oscimg.oschina.net/oscnet/up-96427ee08fca29d77934cfc8d1b1a637cef.png"/></td>
		<td><img src="https://oscimg.oschina.net/oscnet/up-5fdadc582d24cccd7727030d397b63185a3.png"/></td>
    </tr>
	<tr>
        <td><img src="https://oscimg.oschina.net/oscnet/up-0a36797b6bcc50c36d40c3c782665b89efc.png"/></td>
        <td><img src="https://oscimg.oschina.net/oscnet/up-d77995cc00687cedd00d5ac7d68a07ea276.png"/></td>
		<td><img src="https://oscimg.oschina.net/oscnet/up-fa8f5ab20becf59b4b38c1b92a9989e7109.png"/></td>
    </tr>
</table>
