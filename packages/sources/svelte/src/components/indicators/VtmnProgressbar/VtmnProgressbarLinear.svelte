<script>
  import { cn } from '../../../utils/classnames';
  import { VTMN_PROGRESSBAR_SIZE } from './enums';

  /**
   * @type {string} label display above the progress bar.
   * Hidden when indeterminate is true
   * @requires
   */
  export let label;

  /**
   * @type {'small'|'medium'|'large'} size of the progressbar
   * @default medium
   */
  export let size = VTMN_PROGRESSBAR_SIZE.MEDIUM;

  /**
   * @type {number} progress value
   * @default 0
   */
  export let progress;

  /**
   * @type {boolean} Set the progressbar to indeterminate
   * @default false
   */
  export let indeterminate = false;

  let className = undefined;
  /**
   * @type {string} Custom classes to apply to the component.
   */
  export { className as class };

  $: componentClass = cn(
    'vtmn-progressbar_container',
    size && `vtmn-progressbar_size--${size}`,
    indeterminate && `vtmn-progressbar--indeterminate`,
    className,
  );
</script>

<div
  class={componentClass}
  role="progressbar"
  aria-valuemin="0"
  aria-valuemax="100"
  aria-valuenow={indeterminate ? undefined : progress}
  {...$$restProps}
>
  {#if label && !indeterminate}
    <span class="vtmn-progressbar_label" data-value={progress}>{label}</span>
  {/if}
  <svg>
    <line
      class="vtmn-progressbar_indicator"
      x1="0"
      x2={`${indeterminate ? 100 : progress}%`}
      y1="50%"
      y2="50%"
    />
  </svg>
</div>
