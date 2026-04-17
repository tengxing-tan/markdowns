```ts
describe('Test name', () => {
	let spectator: Spectator<MovementOverviewDialogComponent>;
	
	const createComponent = createComponentFactory({
	component: MovementOverviewDialogComponent,
	imports: [DialogModule, InfoHelpModule, ButtonComponent], // add if test failed
	providers: [
	  // add your DI here
	  provideHttpClient(), // for routed page
	  DecimalPipe, // all the pipes being used
	  { provide: DIALOG_DATA, useValue: dialogData }, // need this for dialog component
	],
	componentMocks: [FgMessageService, OverlayRef], // depends, only add if test failed
	});
	
	beforeEach(() => {
    jest
      .spyOn(MovementOverviewDialogComponent.prototype, 'getMovementOverviewData')
      .mockImplementation(() => {}); // if the function is run on ngOnInit

    spectator = createComponent({
	    props: inputBinding
    });
    jest.spyOn(spectator.component.overlayRef, 'detach'); // for dialog component
    spectator.component.movementOverview = { ...({} as MovementOverview), rows: [movementRow] }; // initialize property
  });
  
  it('should init', () => {
    expect(spectator).toBeTruthy();
  });
  
  it('should clear customDescription if user did not change it', () => {
    spectator.component.updateMovementOverviewRows(movementRow, false, 0);
    expect(spectator.component.movementOverview.rows[0].customDescription).toEqual<string>('');
  });
});
```

# Testing pipe
```ts
import { createPipeFactory, SpectatorPipe } from '@ngneat/spectator/jest';

import { ElementLayout } from '@fg/api';

import { HeaderStylingPipe } from './header-styling.pipe';

describe('HeaderStylingPipe', () => {
  let spectator: SpectatorPipe<HeaderStylingPipe>;

  const createPipe = createPipeFactory({
    pipe: HeaderStylingPipe,
    template: `{{ prop | fgHeaderStyling }}`,
  });

  it('should return true for element layout Default', () => {
    spectator = createPipe({
      hostProps: { prop: { index: 2, elementLayout: ElementLayout.Default } },
    });
    expect(spectator.element.innerHTML).toBeTruthy;
  });

  it('should return true for element layout HeaderNotes01', () => {
    spectator = createPipe({
      hostProps: { prop: { index: 2, elementLayout: ElementLayout.HeaderNotes01 } },
    });
    expect(spectator.element.innerHTML).toBeTruthy;
  });

  it('should return true for element layout HeaderNotes02', () => {
    spectator = createPipe({
      hostProps: { prop: { index: 2, elementLayout: ElementLayout.HeaderNotes02 } },
    });
    expect(spectator.element.innerHTML).toBeTruthy;
  });

  it('should return false for valid entry conditions', () => {
    spectator = createPipe({
      hostProps: { prop: { index: 2, elementLayout: ElementLayout.Total01 } },
    });
    expect(spectator.element.innerHTML).toBeFalsy;
  });
});
```
